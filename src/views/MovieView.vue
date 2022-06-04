<template>
  <HeaderCont />
  <main id="main">
    <section class="contact__cont">
      <TitleCont name1="Movie" name2="reference" />
      <div class="contact__cont"></div>
      <ContactCont />
    </section>
  </main>
  <FooterCont />
</template>

<script>
import HeaderCont from "@/components/HeaderCont.vue";
import FooterCont from "@/components/FooterCont.vue";
import TitleCont from "@/components/TitleCont.vue";
import ContactCont from "@/components/ContactCont.vue";

export default {
  components: {
    HeaderCont,
    FooterCont,
    TitleCont,
    ContactCont,
  },
};
</script>

<style lang="scss" scoped></style>
