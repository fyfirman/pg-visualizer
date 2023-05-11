<script setup lang="ts">
import { reactive, ref } from "vue";
import PevVue from '../components/Pev.vue';
import Button from 'primevue/button';
import Dialog from 'primevue/dialog';
import InputText from 'primevue/inputtext';
import Textarea from 'primevue/textarea';

const visible = ref(false);
const label = ref(`Query Plan ${new Date().toISOString()}`);
const queryPlan = ref('');
const query = ref('');
const componentKey = ref(0);

const pevFinalData = reactive({
  plan: "Seq Scan on empty_plan  (cost=0.00..155.00 rows=10000 width=4)",
  query: '',
  label: `Query Plan ${new Date().toISOString()}`,
});
function toggleVisible() {
  visible.value = !visible.value;
}

function savePlan(){
  pevFinalData.plan = queryPlan.value;
  pevFinalData.query = query.value;
  pevFinalData.label = label.value ? label.value : `Query Plan ${new Date().toISOString()}`;

  toggleVisible();
  componentKey.value += 1;
}
</script>

<template>
  <main>
    <div class="header">
      <h1>
        {{ pevFinalData.label }}
      </h1>
      <Button label="Edit Plan" size="small" class="edit-plan-btn" @click="toggleVisible" />
    </div>
    <PevVue :key="componentKey" :plan="pevFinalData.plan" :query="query"/>
    <Dialog
      v-model:visible="visible"
      modal
      header="Edit Plan"
      :style="{ width: '1024px' }"
    >
      <span class="d-flex flex-column w-100">
        <label for="label" class="form-label">Label (Optional)</label>
        <InputText id="label" v-model="label" class="w-100" />
      </span>
      <span class="d-flex flex-column mt-2 w-100">
        <label class="form-label">Plan (JSON)</label>
        <Textarea v-model="queryPlan" rows="5" cols="30" class="w-100 query-plan-text-area" />
      </span>
      <span class="d-flex flex-column mt-2 w-100">
        <label class="form-label">Query</label>
        <Textarea v-model="query" rows="5" cols="30" class="w-100 query-text-area" />
      </span>
      <Button label="Save" class="mt-2" @click="savePlan"/>
    </Dialog>
  </main>
</template>

<style scoped lang="scss">
  .header {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    background-color: #f8f9fa;
    padding: 8px;
    border-bottom: 1px solid #dee2e6;

    h1 {
      font-size: 16px;
      font-weight: 600;
      margin-bottom: 0;
    }

    .edit-plan-btn {
      padding: 4px 8px;
      background-color: #007bff;
      font-family: Noto Sans,sans-serif;
    }
  }
  .form-label {
    font-size: 12px;
    margin-bottom: 0;
  }

  .query-plan-text-area {
    font-family: monospace;
    height: 30vh;
  }

  .query-text-area {
    font-family: monospace;
    height: 10vh;
  }

</style>