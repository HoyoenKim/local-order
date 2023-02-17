<template>
  <q-page class="flex-center bg-grey-4">
    <div>
      <q-carousel
        animated
        swipeable
        infinite
        navigation
        navigation-position="bottom"
        :autoplay="autoplay"
        transition-prev="slide-right"
        transition-next="slide-left"
        @mouseenter="autoplay = false"
        @mouseleave="autoplay = true"
        v-model="slide"
        height="250px"
      >
        <q-carousel-slide
          name="first"
          img-src="https://cdn.quasar.dev/img/mountains.jpg"
        >
        </q-carousel-slide>
        <q-carousel-slide
          name="second"
          img-src="https://cdn.quasar.dev/img/parallax1.jpg"
        >
        </q-carousel-slide>
        <q-carousel-slide
          name="third"
          img-src="https://cdn.quasar.dev/img/parallax2.jpg"
        >
        </q-carousel-slide>
      </q-carousel>
    </div>
    <div>
      <q-card flat class="q-pt-md my-card">
        <q-card-section class="text-h5 text-bold text-center">
          {{ storeName }}
          <q-btn flat round color="red" icon="favorite" />
          <q-btn flat round color="accent" icon="bookmark" />
          <q-btn flat round color="primary" icon="share" />
        </q-card-section>
        <q-separator />
        <q-card-actions vertical class="justify-around"> </q-card-actions>
      </q-card>
    </div>
    <div>{{ storeName }}</div>
    <div class="q-py-md flex-center column q-gutter-md">
      <div class="col">
        <CoffeeCard
          :title="blanceTitle"
          :option="blanceOption"
          :price="blancePrice"
          :explain="blanceLorem"
          :explainLink="blanceExplainLink"
        ></CoffeeCard>
      </div>
      <div class="col">
        <CoffeeCard
          :title="singleTitle"
          :option="singleOption"
          :price="singlePrice"
          :explain="signleLorem"
          :explainLink="singleExplainLink"
        ></CoffeeCard>
      </div>
    </div>
  </q-page>
</template>

<script>
import { defineComponent, ref } from "vue";
import { useCurrentStore } from "stores/currentStore";
import { storeToRefs } from "pinia";
import CoffeeCard from "components/CoffeeCard.vue";

export default defineComponent({
  name: "MenuPage",
  components: {
    CoffeeCard,
  },
  setup() {
    const store = useCurrentStore();
    // use destructuring to use the store in the template
    const { storeName } = storeToRefs(store); // state and getters need "storeToRefs"
    const { increment } = store; // actions can be destructured directly

    return {
      storeName,
      increment,
      slide: ref("first"),
      autoplay: ref(true),
      blanceOption: "Option One",
      blanceTitle: "밸런스 블랜딩",
      blancePrice: "3500 won",
      blanceExplainLink:
        "https://typer.notion.site/e22619aaa3244bef811a0eb97529a7e3",
      blanceLorem:
        "국내 정상급 바리스타가 만든 최고급 품종의 게이샤 원두, &nbsp; 그리고 게이샤 원두와 최적의 조화를 이루는 헤리움 품종의 원두를 섞어 내린 고급 블랜디드 커피입니다.",
      singleOption: "Option Two",
      singleTitle: "싱글 오리진",
      singlePrice: "4000 won",
      singleExplainLink:
        "https://typer.notion.site/cd9823651223426e80d146d16f37d133",
      signleLorem:
        "국내 정상급 로스터가 최고급 생두를 선점하고 로스팅하여 만든 원두 입니다. 단 한 종류의 원두만을 최고급 원두를 골라내 원두의 맛을 극한까지 끌어내기 위한 노력을 기울였습니다.",
    };
  },
});
</script>