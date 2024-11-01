<template>
    <div id="comments-section" class="comments-section"></div>
  </template>
  
  <script setup>
  import { onMounted, onUnmounted } from 'vue'
  
  onMounted(() => {
    console.log("Comments component mounted");
  
    const existingScript = document.getElementById('comments-script');
    if (existingScript) existingScript.remove();
  
    const script = document.createElement('script');
    script.src = "https://utteranc.es/client.js";
    script.id = 'comments-script';
    script.setAttribute('repo', "NanaCs08/Tarea2_Arqui");
    script.setAttribute('issue-term', "pathname");
    script.setAttribute('theme', "github-dark");
    script.setAttribute('crossorigin', "anonymous");
    script.async = true;
    document.getElementById('comments-section').appendChild(script);
  });
  
  onUnmounted(() => {
    const script = document.getElementById('comments-script');
    if (script) script.remove();
  });
  </script>
  