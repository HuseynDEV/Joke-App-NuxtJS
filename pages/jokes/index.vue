<template>
  <div>
     <form @submit.prevent="onSubmit">
      <input placeholder="Search joke" v-model="text" />
      <input type="submit" value="Search" name="" id="" />
    </form>
    <Joke
      v-for="joke in jokes"
      :key="joke.id"
      :joke="joke.joke"
      :id="joke.id"
    />
  </div>
</template>

<script>
import Joke from "@/components/Joke";

export default {
  components: {
    Joke,

  },
  data() {
    return {
      jokes: [],
      text:''
    };
  },
  async created() {
    const config = {
      headers: {
        Accept: "application/json",
      },
    };
    try {
      const res = await this.$axios.get(
        "https://icanhazdadjoke.com/search",
        config
      );
      this.jokes = res.data.results;
      //  console.lo
    } catch (err) {
      console.log(err);
    }
  },
  methods: {
    async onSubmit() {
        const config = {
          headers: {
            Accept: "application/json",
          },
        };
        try {
          const res = await this.$axios.get(
            `https://icanhazdadjoke.com/search?term=${this.text}`,
            config
          );
          this.jokes = res.data.results;
          //  console.lo
        } catch (err) {
          console.log(err);
        }
    },
  },
};
</script>
