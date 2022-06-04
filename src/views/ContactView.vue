<template>
  <HeaderCont />
  <main id="main">
    <section class="contact__cont">
      <div class="contact__inner">
        <div v-for="title in titles" v-bind:key="title.text">
          {{ title.text }}
        </div>
      </div>
    </section>
  </main>
  <FooterCont />
</template>

<script>
import HeaderCont from "@/components/HeaderCont.vue";
import FooterCont from "@/components/FooterCont.vue";

export default {
  components: {
    HeaderCont,
    FooterCont,
  },

  data: function () {
    return {
      titles: [
        { text: "you are" },
        { text: "already" },
        { text: "doing well." },
      ],
    };
  },
};
</script>
<style lang="scss" scoped>
.contact__cont {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background: var(--dark_bg);

  .contact__inner {
    font-size: 10vw;
    line-height: 0.85;
    font-family: var(--main_font);
    color: var(--white);
    text-transform: uppercase;
  }
}
</style>
