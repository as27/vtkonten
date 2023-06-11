<script setup>
import { computed } from '@vue/reactivity';

const props = defineProps({
  kontoname: {
    type: String,
    required: true
  },
  buchungen: {
    type: Array
  }
})
const sumsoll = computed(() => {
  var sum = 0;
  props.buchungen.forEach((element) => {
    sum = sum + Number(element.bsoll);
  })
  return sum;
});

const sumhaben = computed(() => {
  var sum = 0;
  props.buchungen.forEach((element) => {
    sum = sum + Number(element.bhaben);
  })
  return sum;
});
</script>

<template>
  <div class="konto">
  <table>
    <caption>
      {{
        kontoname
      }}
    </caption>
    <tr class="top">
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
    <tr v-for="buchung in buchungen">
      <td class="btext">{{ buchung.tsoll }}</td>
      <td class="bbtr">{{ buchung.bsoll }}</td>
      <td class="center btext">{{ buchung.thaben }}</td>
      <td class="bbtr">{{ buchung.bhaben }}</td>
    </tr>
    <tr>
      <td></td>
      <td class="bbtr">{{ sumsoll }}</td>
      <td></td>
      <td class="bbtr">{{ sumhaben }}</td>
    </tr>
  </table>
</div>
</template>

<style scoped>
table {
  border-collapse: collapse;
  border-spacing: 0;
  margin:auto;
}

div.konto {
  float:left;
  box-shadow: 3px 3px 5px lightgray;
  width: 400px;
  border: 1px solid #e1e1e1;
  border-radius: 5px;
  padding: 3px;
  margin-right: 0.5em;
  margin-bottom: 1em;
}

caption{
  font-weight: bold;
}
.top th {
  border-bottom: 3px solid black;
}

th {
  font-weight: bold;
}

td {
  width: 25%;
  padding: 0;
  margin: 0;
}

.center {
  border-left: 3px solid black;
}

.bbtr {
  text-align: right;
  padding-right: 0.3em;
}

.btext {
  padding-left: 0.3em;
}
</style>
