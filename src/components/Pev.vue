<script lang="ts">
import { Plan } from "pev2"
import "pev2/dist/style.css"
import { ref } from "vue";

const plan = "Seq Scan on empty_plan  (cost=0.00..155.00 rows=10000 width=4)";
const error = ref(false)

export default {
  name: "PEV2 example",
  props: {
    plan: {
      type: String,
      default: plan,
    },
    query: {
      type: String,
      default: ''
    }
  },
  components: {
    pev2: Plan,
  },
  setup() {
    return {
      error,
    }
  },
  errorCaptured(err: any, vm: any, info: any) {
    error.value = true;
    console.error(err, vm, info);
    return false;
  },
}

</script>

<template>
  <pev2 v-if="!error" :plan-source="plan" :plan-query=query />
  <div v-else>
    <h1>PEV2</h1>
    <p>There was an error loading the plan.</p>
  </div>
</template>