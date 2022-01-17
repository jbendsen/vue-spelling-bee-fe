<template>
  <div class="container">
    <div class="py-5 text-center">
      <img
        class="d-block mx-auto mb-4"
        src="https://compote.slate.com/images/edb13794-48d9-4c0d-972d-324760e03e2a.jpeg?width=400&rect=1560x1040&offset=0x0"
        alt=""
      />
      <h2>Spelling bee</h2>
      <p class="lead">Here you can get help with Spelling Bee puzzles</p>
    </div>
    <div class="text-left">
      <form @submit.prevent="submitForm">
        <div class="form-group">
          <label for="letters">Letters</label>
          <input
            type="text"
            class="form-control"
            v-model="letters"
            id="letters"
            placeholder="Enter 7 letters"
            size="7"
          />
          <small id="emailHelp" class="form-text text-muted"
            >Sequence and casing is arbitrary</small
          >
        </div>
        <div class="form-group">
          <label for="mandatory">Mandatory letter</label>
          <input
            type="text"
            class="form-control"
            v-model="mandatory"
            id="mandatory"
            placeholder="Enter mandatory letter"
            size="1"
          />
        </div>
        <!-- <input type="checkbox" class="form-check-input" id="exampleCheck1" /> -->

        <button type="submit" class="btn btn-primary">Submit</button>
      </form>
    </div>
    <div class="mt-3" v-if="words.length>0">
      <h3>Matching words:</h3>
      <ul id="letters" class="list-group">
        <li class="list-group-item" v-for="word in words" :key="word">
          {{ word }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "LettersForm",
  props: {},
  data() {
    return {
      letters: "",
      mandatory: "",
      words: [],
    };
  },
  methods: {
    // submit the form to our backend api
    async submitForm() {
      console.log("submit");
      console.log(
        "https://zckpf6sdvj.execute-api.eu-west-1.amazonaws.com/default/function-go-function-DaGnyXFmx5pd?letters=" +
          this.letters +
          "&mandatory=" +
          this.mandatory
      );

      await fetch(
        "https://zckpf6sdvj.execute-api.eu-west-1.amazonaws.com/default/function-go-function-DaGnyXFmx5pd?letters=" +
          this.letters +
          "&mandatory=" +
          this.mandatory,
        {
          method: "GET",
        }
      )
        .then((res) => res.json())
        .then((res) => {
          this.words = res.words;
        });
    },
  },
};
</script>

