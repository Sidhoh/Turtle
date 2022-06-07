<template>
  <div v-on:keyup.esc="open">
    <textarea
      id="editor"
      placeholder="Start Typing..."
      v-model="input"
      @input="render"
      spellcheck="false"
    />
    <div class="result" v-html="output" />
    <div>
      <button class="menu" v-on:click="open">
        <svg
          title="Menu"
          xmlns="http://www.w3.org/2000/svg"
          xmlns:xlink="http://www.w3.org/1999/xlink"
          aria-hidden="true"
          role="img"
          class="iconify iconify--ph"
          width="40"
          height="40"
          preserveAspectRatio="xMidYMid meet"
          viewBox="0 0 256 256"
        >
          <path
            fill="#888888"
            d="m117.3 134l-72 64a8.1 8.1 0 0 1-5.3 2a8 8 0 0 1-5.3-14l65.3-58l-65.3-58a8 8 0 1 1 10.6-12l72 64a8 8 0 0 1 0 12Zm98.7 50h-96a8 8 0 0 0 0 16h96a8 8 0 0 0 0-16Z"
          ></path>
        </svg>
      </button>
      <button class="download" v-if="actions" v-on:click="download">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          xmlns:xlink="http://www.w3.org/1999/xlink"
          aria-hidden="true"
          role="img"
          class="iconify iconify--material-symbols"
          width="32"
          height="32"
          preserveAspectRatio="xMidYMid meet"
          viewBox="0 0 24 24"
        >
          <path
            fill="#888888"
            d="m12 16l-5-5l1.4-1.45l2.6 2.6V4h2v8.15l2.6-2.6L17 11Zm-6 4q-.825 0-1.412-.587Q4 18.825 4 18v-3h2v3h12v-3h2v3q0 .825-.587 1.413Q18.825 20 18 20Z"
          ></path>
        </svg>
      </button>
      <input
        type="file"
        class="import"
        v-if="actions"
        @change="openFile"
        solo
      />
      <p class="import-wrap" v-if="actions" />
      <button class="about" v-if="actions" v-on:click="about">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          xmlns:xlink="http://www.w3.org/1999/xlink"
          aria-hidden="true"
          role="img"
          class="iconify iconify--material-symbols"
          width="32"
          height="32"
          preserveAspectRatio="xMidYMid meet"
          viewBox="0 0 24 24"
        >
          <path
            fill="#888888"
            d="M12 17q.425 0 .713-.288Q13 16.425 13 16v-4.025q0-.425-.287-.7Q12.425 11 12 11t-.712.287Q11 11.575 11 12v4.025q0 .425.288.7q.287.275.712.275Zm0-8q.425 0 .713-.288Q13 8.425 13 8t-.287-.713Q12.425 7 12 7t-.712.287Q11 7.575 11 8t.288.712Q11.575 9 12 9Zm0 13q-2.075 0-3.9-.788q-1.825-.787-3.175-2.137q-1.35-1.35-2.137-3.175Q2 14.075 2 12t.788-3.9q.787-1.825 2.137-3.175q1.35-1.35 3.175-2.138Q9.925 2 12 2t3.9.787q1.825.788 3.175 2.138q1.35 1.35 2.137 3.175Q22 9.925 22 12t-.788 3.9q-.787 1.825-2.137 3.175q-1.35 1.35-3.175 2.137Q14.075 22 12 22Zm0-10Zm0 8q3.325 0 5.663-2.337Q20 15.325 20 12t-2.337-5.663Q15.325 4 12 4T6.338 6.337Q4 8.675 4 12t2.338 5.663Q8.675 20 12 20Z"
          ></path>
        </svg>
      </button>
    </div>
  </div>
</template>

<script>
import { marked } from "marked";
import { saveAs } from "file-saver";

export default {
  name: "App",
  components: {},
  data() {
    return {
      actions: false,
      output: "",
      input: "",
    };
  },
  methods: {
    render: function () {
      this.output = marked(this.input);
    },
    open: function () {
      this.actions = !this.actions;
    },
    download: function () {
      var blob = new Blob([this.input], {
        type: "text/plain;charset=utf-8",
      });
      saveAs(blob, "Turtle.md");
    },
    openFile: function (e) {
      console.log(e.target.files[0]);
      let file = e.target.files[0];
      let reader = new FileReader();
      reader.readAsText(file, "UTF-8");
      reader.onload = (evt) => {
        this.input = evt.target.result;
        this.output = marked(this.input);
      };
    },
    about: function () {
      this.input = `# _Tutle_
Is a rework of  [goo](https://www.goo.sidhh.online/) with new changes like new theme, menu bar and file system.

Pressing **ESC** opens up the menu bar where you can access save, open, and about menus.

⟨/⟩ with ♥ & VueJS, by [Sidh](https://github.com/sidhoh)`;
      this.output = marked(this.input);
    },
  },
  mounted() {
    if (localStorage.input) {
      this.input = localStorage.input;
      this.output = marked(this.input);
    }
  },
  watch: {
    input(input) {
      localStorage.input = input;
    },
  },
};
</script>
