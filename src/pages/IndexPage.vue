<template>
  <q-page class="">
    <div class="row q-col-gutter-md q-pa-md">
      <div class=" col"> <q-select square dense outlined v-model="modelSelect" :options="options" label="Estados">
          <template v-slot:prepend>
            <q-icon name="sort" class="cursor-pointer">
            </q-icon></template></q-select></div>
      <div class="col"> <q-input square dense label="Início" outlined v-model="dateStart" :mask="dateMask">
          <template v-slot:append>
            <q-icon name="event" class="cursor-pointer">
              <q-popup-proxy cover transition-show="scale" transition-hide="scale">
                <q-date v-model="dateStart" color="green-9" :mask="date">
                  <div class="row items-center justify-end">
                    <q-btn v-close-popup label="Confirmar" color="primary" flat />
                  </div>
                </q-date>
              </q-popup-proxy>
            </q-icon>
          </template>
        </q-input></div>
      <div class="col"> <q-input square dense label="Fim" outlined v-model="dateEnd" :mask="dateMask">
          <template v-slot:append>
            <q-icon name="event" class="cursor-pointer">
              <q-popup-proxy cover transition-show="scale" transition-hide="scale">
                <q-date v-model="dateEnd" color="blue-9" :mask="date">
                  <div class="row items-center justify-end">
                    <q-btn v-close-popup label="Confirmar" color="primary" flat />
                  </div>
                </q-date>
              </q-popup-proxy>
            </q-icon>
          </template>
        </q-input></div>
      <div class="col-3"> <q-btn class=" float-right" color="grey-9" icon="search" label="Pesquisar" square /></div>
    </div>

    <div class="row">
      <q-table class="col" flat bordered title="Treats" dense :rows="rows" :columns="columns" row-key="name"
        :filter="filter">

        <template v-slot:top>
          <div class="col-12">
            <q-input borderless color="grey-9" dense debounce="300" v-model="filter" placeholder="Pesquisar">
              <template v-slot:append>
                <q-btn v-if="filter" icon="clear" size="md" @click="() => { filter = null }" dense round color="grey-9"
                  flat></q-btn>
                <q-icon v-else name="search" />
              </template>

            </q-input>

          </div>
          <div class="col-12 q-mt-xs">
            <q-separator size="lg" color="grey-3"></q-separator>
          </div>
        </template> <template v-slot:body-cell-actions="props">
          <q-td :props="props" class="q-gutter-xs">
            <q-btn color="red-9" icon="delete" class="float-right" size="sm" round />
            <q-btn color="orange" icon="edit" class="float-right" size="sm" round />
          </q-td>
        </template>
        <template v-slot:body-cell-select="props">
          <q-td :props="props" class="q-gutter-xs">
            <q-btn color="grey" icon="visibility" outline class="float-left" size="sm" round />
          </q-td>
        </template>
        <template v-slot:loading>
          <q-inner-loading showing color="grey-5" label="Processando" label-class="text-grey-6" />
        </template></q-table>

      <!--  <q-markup-table dense v-else class="shadow-0 col bg-transparent">
    <thead>
      <tr>
        <th class="text-left" style="width: 150px">
          <q-skeleton animation="blink" type="text" />
        </th>
        <th class="text-right">
          <q-skeleton animation="blink" type="text" />
        </th>
        <th class="text-right">
          <q-skeleton animation="blink" type="text" />
        </th>
        <th class="text-right">
          <q-skeleton animation="blink" type="text" />
        </th>


      </tr>
    </thead>

    <tbody>
      <tr v-for="n in 17" :key="n">
        <td class="text-left">
          <q-skeleton animation="blink" type="text" width="85px" />
        </td>
        <td class="text-right">
          <q-skeleton animation="blink" type="text" width="50px" />
        </td>
        <td class="text-right">
          <q-skeleton animation="blink" type="text" width="35px" />
        </td>
        <td class="text-right">
          <q-skeleton animation="blink" type="text" width="65px" />
        </td>


      </tr>
    </tbody>
  </q-markup-table> -->
    </div>
  </q-page>
</template>

<script setup>
import { ref } from 'vue'
defineOptions({
  name: 'IndexPage'
});

const options = [
  'Aberto', 'Cancelado', 'Pago'
]
const date = 'DD/MM/YYYY'
const dateMask = '##/##/####'
const modelSelect = ref(null)
const dateStart = ref(null)
const dateEnd = ref(null)
const filter = ref(null)

const columns = [
  {
    name: 'name',
    required: true,
    label: 'Dessert (100g serving)',
    align: 'left',
    field: row => row.name,
    format: val => `${val}`,
    sortable: true
  },
  { name: 'calories', align: 'center', label: 'Calories', field: 'calories', sortable: true },
  { name: 'fat', label: 'Fat (g)', field: 'fat', sortable: true },
  { name: 'carbs', label: 'Carbs (g)', field: 'carbs' },
  { name: 'protein', label: 'Protein (g)', field: 'protein' },
  { name: 'sodium', label: 'Sodium (mg)', field: 'sodium' },
  { name: 'calcium', label: 'Calcium (%)', field: 'calcium', sortable: true, sort: (a, b) => parseInt(a, 10) - parseInt(b, 10) },
  { name: 'iron', label: 'Iron (%)', field: 'iron', sortable: true, sort: (a, b) => parseInt(a, 10) - parseInt(b, 10) }
]

const rows = [
  {
    name: 'Frozen Yogurt',
    calories: 159,
    fat: 6.0,
    carbs: 24,
    protein: 4.0,
    sodium: 87,
    calcium: '14%',
    iron: '1%'
  },
  {
    name: 'Ice cream sandwich',
    calories: 237,
    fat: 9.0,
    carbs: 37,
    protein: 4.3,
    sodium: 129,
    calcium: '8%',
    iron: '1%'
  },
  {
    name: 'Eclair',
    calories: 262,
    fat: 16.0,
    carbs: 23,
    protein: 6.0,
    sodium: 337,
    calcium: '6%',
    iron: '7%'
  },
  {
    name: 'Cupcake',
    calories: 305,
    fat: 3.7,
    carbs: 67,
    protein: 4.3,
    sodium: 413,
    calcium: '3%',
    iron: '8%'
  },
  {
    name: 'Gingerbread',
    calories: 356,
    fat: 16.0,
    carbs: 49,
    protein: 3.9,
    sodium: 327,
    calcium: '7%',
    iron: '16%'
  },
  {
    name: 'Jelly bean',
    calories: 375,
    fat: 0.0,
    carbs: 94,
    protein: 0.0,
    sodium: 50,
    calcium: '0%',
    iron: '0%'
  },
  {
    name: 'Lollipop',
    calories: 392,
    fat: 0.2,
    carbs: 98,
    protein: 0,
    sodium: 38,
    calcium: '0%',
    iron: '2%'
  },
  {
    name: 'Honeycomb',
    calories: 408,
    fat: 3.2,
    carbs: 87,
    protein: 6.5,
    sodium: 562,
    calcium: '0%',
    iron: '45%'
  },
  {
    name: 'Donut',
    calories: 452,
    fat: 25.0,
    carbs: 51,
    protein: 4.9,
    sodium: 326,
    calcium: '2%',
    iron: '22%'
  },
  {
    name: 'KitKat',
    calories: 518,
    fat: 26.0,
    carbs: 65,
    protein: 7,
    sodium: 54,
    calcium: '12%',
    iron: '6%'
  }, {
    name: "actions",
    label: "Ações",
    align: "right",
    field: (row) => row.actions,
  }
]
</script>
