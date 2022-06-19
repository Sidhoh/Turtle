<template>
  <textarea
    id="editor"
    placeholder="Start Typing..."
    v-model="input"
    @input="render"
    spellcheck="false"
  />
  <div class="result" v-html="output" />
  <div class="menu">
    <hr />
    <button class="download" v-on:click="download">
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
          fill="#c5cff5"
          d="m12 16l-5-5l1.4-1.45l2.6 2.6V4h2v8.15l2.6-2.6L17 11Zm-6 4q-.825 0-1.412-.587Q4 18.825 4 18v-3h2v3h12v-3h2v3q0 .825-.587 1.413Q18.825 20 18 20Z"
        ></path>
      </svg>
    </button>
    <label>
      <svg
        xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        aria-hidden="true"
        role="img"
        class="iconify iconify--material-symbols"
        width="30"
        height="30"
        preserveAspectRatio="xMidYMid meet"
        viewBox="0 0 24 24"
      >
        <path
          fill="#c5cff5"
          d="M4 22V2h10l6 6v6h-2V9h-5V4H6v16h9v2Zm17.95.375L19 19.425v2.225h-2V16h5.65v2H20.4l2.95 2.95ZM6 20V4v16Z"
        ></path>
      </svg>
      <input type="file" class="import" @change="openFile" solo />
    </label>
    <button class="about" v-on:click="about">
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
          fill="#c5cff5"
          d="M12 17q.425 0 .713-.288Q13 16.425 13 16v-4.025q0-.425-.287-.7Q12.425 11 12 11t-.712.287Q11 11.575 11 12v4.025q0 .425.288.7q.287.275.712.275Zm0-8q.425 0 .713-.288Q13 8.425 13 8t-.287-.713Q12.425 7 12 7t-.712.287Q11 7.575 11 8t.288.712Q11.575 9 12 9Zm0 13q-2.075 0-3.9-.788q-1.825-.787-3.175-2.137q-1.35-1.35-2.137-3.175Q2 14.075 2 12t.788-3.9q.787-1.825 2.137-3.175q1.35-1.35 3.175-2.138Q9.925 2 12 2t3.9.787q1.825.788 3.175 2.138q1.35 1.35 2.137 3.175Q22 9.925 22 12t-.788 3.9q-.787 1.825-2.137 3.175q-1.35 1.35-3.175 2.137Q14.075 22 12 22Zm0-10Zm0 8q3.325 0 5.663-2.337Q20 15.325 20 12t-2.337-5.663Q15.325 4 12 4T6.338 6.337Q4 8.675 4 12t2.338 5.663Q8.675 20 12 20Z"
        ></path>
      </svg>
    </button>
    <a class="github" href="https://github.com/Sidhoh/Turtle">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        aria-hidden="true"
        role="img"
        class="iconify iconify--teenyicons"
        width="32"
        height="32"
        preserveAspectRatio="xMidYMid meet"
        viewBox="0 0 15 15"
      >
        <path
          fill="#c5cff5"
          d="M5.65 12.477a.5.5 0 1 0-.3-.954l.3.954Zm-3.648-2.96l-.484-.128l-.254.968l.484.127l.254-.968ZM9 14.5v.5h1v-.5H9Zm.063-4.813l-.054-.497a.5.5 0 0 0-.299.852l.352-.354ZM12.5 5.913h.5V5.91l-.5.002Zm-.833-2.007l-.466-.18a.5.5 0 0 0 .112.533l.354-.353Zm-.05-2.017l.456-.204a.5.5 0 0 0-.319-.276l-.137.48Zm-2.173.792l-.126.484a.5.5 0 0 0 .398-.064l-.272-.42Zm-3.888 0l-.272.42a.5.5 0 0 0 .398.064l-.126-.484ZM3.383 1.89l-.137-.48a.5.5 0 0 0-.32.276l.457.204Zm-.05 2.017l.354.353a.5.5 0 0 0 .112-.534l-.466.181ZM2.5 5.93H3v-.002l-.5.002Zm3.438 3.758l.352.355a.5.5 0 0 0-.293-.851l-.06.496ZM5.5 11H6l-.001-.037L5.5 11ZM5 14.5v.5h1v-.5H5Zm.35-2.977c-.603.19-.986.169-1.24.085c-.251-.083-.444-.25-.629-.49a4.8 4.8 0 0 1-.27-.402c-.085-.139-.182-.302-.28-.447c-.191-.281-.473-.633-.929-.753l-.254.968c.08.02.184.095.355.346c.082.122.16.252.258.412c.094.152.202.32.327.484c.253.33.598.663 1.11.832c.51.168 1.116.15 1.852-.081l-.3-.954Zm4.65-.585c0-.318-.014-.608-.104-.878c-.096-.288-.262-.51-.481-.727l-.705.71c.155.153.208.245.237.333c.035.105.053.254.053.562h1Zm-.884-.753c.903-.097 1.888-.325 2.647-.982c.78-.675 1.237-1.729 1.237-3.29h-1c0 1.359-.39 2.1-.892 2.534c-.524.454-1.258.653-2.099.743l.107.995ZM13 5.91a3.354 3.354 0 0 0-.98-2.358l-.707.706c.438.44.685 1.034.687 1.655l1-.003Zm-.867-1.824c.15-.384.22-.794.21-1.207l-1 .025a2.12 2.12 0 0 1-.142.82l.932.362Zm.21-1.207a3.119 3.119 0 0 0-.27-1.195l-.913.408c.115.256.177.532.184.812l1-.025Zm-.726-.99c.137-.481.137-.482.136-.482h-.003l-.004-.002a.462.462 0 0 0-.03-.007a1.261 1.261 0 0 0-.212-.024a2.172 2.172 0 0 0-.51.054c-.425.091-1.024.317-1.82.832l.542.84c.719-.464 1.206-.634 1.488-.694a1.2 1.2 0 0 1 .306-.03l-.008-.001a.278.278 0 0 1-.01-.002l-.006-.002h-.003l-.002-.001c-.001 0-.002 0 .136-.482Zm-2.047.307a8.209 8.209 0 0 0-4.14 0l.252.968a7.209 7.209 0 0 1 3.636 0l.252-.968Zm-3.743.064c-.797-.514-1.397-.74-1.822-.83a2.17 2.17 0 0 0-.51-.053a1.259 1.259 0 0 0-.241.03l-.004.002h-.003l.136.481l.137.481h-.001l-.002.001l-.003.001a.327.327 0 0 1-.016.004l-.008.001h.008a1.19 1.19 0 0 1 .298.03c.282.06.769.23 1.488.694l.543-.84Zm-2.9-.576a3.12 3.12 0 0 0-.27 1.195l1 .025a2.09 2.09 0 0 1 .183-.812l-.913-.408Zm-.27 1.195c-.01.413.06.823.21 1.207l.932-.362a2.12 2.12 0 0 1-.143-.82l-1-.025Zm.322.673a3.354 3.354 0 0 0-.726 1.091l.924.38c.118-.285.292-.545.51-.765l-.708-.706Zm-.726 1.091A3.354 3.354 0 0 0 2 5.93l1-.003c0-.31.06-.616.177-.902l-.924-.38ZM2 5.93c0 1.553.458 2.597 1.239 3.268c.757.65 1.74.88 2.64.987l.118-.993C5.15 9.09 4.416 8.89 3.89 8.438C3.388 8.007 3 7.276 3 5.928H2Zm3.585 3.404c-.5.498-.629 1.09-.584 1.704L6 10.963c-.03-.408.052-.683.291-.921l-.705-.709ZM5 11v3.5h1V11H5Zm5 3.5V13H9v1.5h1Zm0-1.5v-2.063H9V13h1Z"
        ></path>
      </svg>
    </a>
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
      output: "",
      input: "",
    };
  },
  methods: {
    render: function () {
      this.output = marked(this.input);
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

⟨/⟩ with ♥ & VueJS, by [SIdh](https://github.com/sidhoh)`;
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
