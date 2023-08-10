<template>
  <main>
    <h1>Local Markdown Generator</h1>
    <br>
    <section class="markdown">
      <textarea class="markdown-source" v-model="source"></textarea>
      <br>
      <hr class="dotted">
      <br>
      <div class="markdown-render" v-html="markdown.render(source)" />
    </section>
  </main>
</template>

<script setup>
import { ref, watch, onMounted } from 'vue'
import MarkdownIt from "markdown-it";
import MarkdownItAbbr from "markdown-it-abbr";
import MarkdownItHighlightjs from "markdown-it-highlightjs";

const markdown = new MarkdownIt()
  .use(MarkdownItAbbr)
  .use(MarkdownItHighlightjs),

  source = ref('This is a test')

onMounted(() => {
  source.value = localStorage.getItem("mdSource");
})

watch(source, () => {
  localStorage.setItem("mdSource", source.value);
})

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.markdown {
  display: flex;
  padding: 25px 0;
}

.markdown-source {
  width: 35%;
  height: 100vh;
  border: none;
}

.markdown-render {
  width: 65%;
  height: 100vh;
  text-align: left;
}

.dotted {
  margin: 10px;
}
</style>
