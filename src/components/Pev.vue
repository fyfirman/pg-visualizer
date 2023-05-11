<script>
import { Plan } from "pev2"
import "pev2/dist/style.css"

const plan = "Seq Scan on foo  (cost=0.00..155.00 rows=10000 width=4)";

export default {
  name: "PEV2 example",
  components: {
    pev2: Plan,
  },
  data() {
    return {
      plan: plan,
    }
  },
}

</script>

<template>
  <pev2 :plan-source="plan" plan-query="" />
</template>