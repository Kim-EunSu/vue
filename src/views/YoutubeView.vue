<template>
  <HeaderCont />
  <main id="main">
    <section class="youtube__cont">
      <TitleCont name1="youtube" name2="reference" />
      <div class="youtube__cont"></div>
    </section>
  </main>
  <FooterCont />
</template>

<script>
import HeaderCont from "@/components/HeaderCont.vue";
import FooterCont from "@/components/FooterCont.vue";
import TitleCont from "@/components/TitleCont.vue";

export default {
  components: {
    HeaderCont,
    FooterCont,
    TitleCont,
  },
};
</script>

<style lang="scss" scoped></style>
