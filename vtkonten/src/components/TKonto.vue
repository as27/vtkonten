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

const kontobuchungen = computed(() => {
  const kb = [];
  props.buchungen.forEach((element,index) => {
    const b = {
      zeile: element.zeile,
      tsoll: '',
      bsoll: '',
      thaben: '',
      bhaben: '',
      color: ''
    };
    if (element.ksoll == props.kontoname) {
        b.tsoll= element.text;
        b.bsoll= element.btrsoll;
        b.color= element.color
    }
    if (element.khaben == props.kontoname) {
        b.thaben= element.text;
        b.bhaben= element.btrhaben;
        b.color= element.color
    }
    kb.push(b);
  })
  return kb;
})
const sumsoll = computed(() => {
  if (kontobuchungen === null){
    return 0;
  }
  var sum = 0;
  kontobuchungen.value.forEach((element) => {
    sum = sum + Number(element.bsoll);
  })
  return sum;
});

const sumhaben = computed(() => {
  if (kontobuchungen === null){
    return 0;
  }
  var sum = 0;
  kontobuchungen.value.forEach((element) => {
    sum = sum + Number(element.bhaben);
  })
  return sum;
});
</script>

<template>
  <div class="konto">
    <table>
      <tr class="top">
        <th class="linenr"></th>
        <th class="line" colspan="4">{{ kontoname }}</th>
      </tr>
      <tr v-for="buchung in kontobuchungen" 
      :style="{'background-color': buchung.color}"
      >
        <td class="linenr">{{ buchung.zeile }}</td>
        <td class="btext">{{ buchung.tsoll }}</td>
        <td class="bbtr">{{ buchung.bsoll }}</td>
        <td class="center btext">{{ buchung.thaben }}</td>
        <td class="bbtr">{{ buchung.bhaben }}</td>
      </tr>
      <tr>
        <td></td>
        <td></td>
        <td class="bbtr sum">{{ sumsoll }}</td>
        <td></td>
        <td class="bbtr sum">{{ sumhaben }}</td>
      </tr>
    </table>
  </div>
</template>

<style scoped>
table {
  border-collapse: collapse;
  border-spacing: 0;
  margin: auto;
}

div.konto {
  float: left;
  box-shadow: 3px 3px 5px lightgray;
  width: 400px;
  border: 1px solid #e1e1e1;
  border-radius: 5px;
  padding: 1em;
  margin-right: 0.5em;
  margin-bottom: 1em;
}

caption {
  font-weight: bold;
}

.top th.line {
  border-bottom: 3px solid black;
}

th {
  padding: 0px;
  font-weight: bold;
  text-align: center;
}
td.linenr {
  width: 20px;
  text-align: center;
  border-bottom: 0px;
}

td {

  border-bottom: 1px dotted #eaeaea;
}



.center {
  border-left: 3px solid black;
}

.bbtr {
  width: 60px;
  text-align: right;
  padding-right: 0.3em;
}

.btext {
  width: 200px;
  padding-left: 0.3em;
}

.sum {
  font-weight: bold;
}
</style>
