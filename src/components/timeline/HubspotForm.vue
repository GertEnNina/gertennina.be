<template>
    <div :id="'hubspotForm_' + name.split(' ')[0]" v-once></div>
</template>

<script>
/* eslint-disable vue/multi-word-component-names */

export default {
  name: 'HubspotForm',
  props: {formType: String, name: String},
  data() {
    return {

    }
  },
  watch: {

  },
  computed: {

  },
  mounted() {
    const script = document.createElement("script");
    script.src = "https://js-eu1.hsforms.net/forms/v2.js";
    document.body.appendChild(script);
    script.addEventListener("load", () => {
      if (window.hbspt) {
        switch (this.formType) {
          case "full":
            window.hbspt.forms.create({
              css: '',
              region: "eu1",
              portalId: "140826681",
              formId: "cc7b38ce-30ce-49f4-b1c6-0ae6acba6eb8",
              target: "#hubspotForm_" + this.name.split(' ')[0],
              onFormReady: function(form){
                form.elements['name_guest'].value = this.name;
              }.bind(this)
          })
          break;
          case "partial":
            window.hbspt.forms.create({
              css: '',
              region: "eu1",
              portalId: "140826681",
              formId: "cc4c0497-9560-4fec-bb0a-bed0e35c1d1c",
              target: "#hubspotForm_" + this.name.split(' ')[0],
              onFormReady: function(form){
                form.elements['name_guest'].value = this.name;
              }.bind(this)
          })
          break;
          case "receptie":
            window.hbspt.forms.create({
              css: '',
              region: "eu1",
              portalId: "140826681",
              formId: "1cb838f1-9ea3-4a1f-8a66-d9f9ec09d946",
              target: "#hubspotForm_" + this.name.split(' ')[0],
              onFormReady: function(form){
                form.elements['name_guest'].value = this.name;
              }.bind(this)
          })
          break;
          case "all":
            window.hbspt.forms.create({
              css: '',
              region: "eu1",
              portalId: "140826681",
              formId: "d759a50b-c141-4c16-acf2-a81fef905bfc",
              target: "#hubspotForm_" + this.name.split(' ')[0],
              onFormReady: function(form){
                form.elements['name_guest'].value = this.name;
              }.bind(this)
          })
          break;
        }
      }

    });
  }
}
</script>

<style scoped>

</style>
