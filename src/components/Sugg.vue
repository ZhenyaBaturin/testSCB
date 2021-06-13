<template>
  <div class="form-living_input">
    <VueSuggestions
      model.sync="city"
      coordinates.sync="coordinates"
      :placeholder="'Адрес регистрации'"
      :class="getClass()"
      class="input cont"
      :disabled="checkbox"
      :options="suggestionOptions"
    >
    </VueSuggestions>
  </div>
</template>
<script>
import VueSuggestions from "vue-suggestions";

export default {
  props: ["checkbox"],
  data() {
    return {
      city: "",
      coordinates: {
        latitude: "",
        longitude: "",
      },
      suggestionOptions: {
        // @see https://confluence.hflabs.ru/pages/viewpage.action?pageId=207454318
        token: "92d9480112e42f8b923c3ad8ea5af68c46222760",
        type: "ADDRESS",
        scrollOnFocus: false,
        triggerSelectOnBlur: false,
        triggerSelectOnEnter: false,
        addon: "none",
        // @see https://confluence.hflabs.ru/pages/viewpage.action?pageId=207454320
        onSelect: (suggestion) => {
          this.get(suggestion);
        },
      },
    };
  },
  methods: {
    getClass() {
      return {
        hidden: this.checkbox,
        "fa-checkbox-blank-outline": !this.checkbox,
      };
    },
    get(obj) {
      this.$emit("arrayData", obj);
    },
  },
  components: { VueSuggestions },
};
</script>

<style>
.hidden {
  background-color: #e0dede !important;
}

.suggestions-wrapper {
  position: relative;
}

.suggestions-suggestions {
  border-color: #d9d9d9 !important;
  border-radius: 3px;
  box-shadow: 0px 3px 5px rgba(0, 0, 0, 0.5);
  top: 7px !important;
  overflow: hidden;
  z-index: 10 !important;
  background-color: rgb(255, 255, 255);
}

.suggestions-suggestion {
  padding-left: 0;
  cursor: pointer;
  font-size: 16px;
  padding-top: 5px !important;
  padding-bottom: 5px !important;
}

.suggestions-suggestion:hover {
  background-color: #b8b4b4;
}

.suggestions-value {
  padding-left: 10px;
  margin: 0;
  font-size: 16px;
}

.input {
  border-radius: 5px;
  box-shadow: none;
  border: 0.5px solid #ced6e0;
  transition: all 0.3s ease-in-out;
  font-size: 13px;
  padding: 15px 15px !important;
  background: none;
  color: #1a3b5d;
  font-family: "Source Sans Pro", sans-serif;
}

.form-living_input {
  width: 66%;
}

.cont {
  width: 100%;
}

@media (max-width: 763px) {
  .form-living_input {
    width: 100% !important;
  }
}
</style>
