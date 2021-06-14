<template>
  <v-container>
    <v-row align="center" justify="center" style="height: 100vh;">
      <v-col cols="12" md="5" xl="4">
        <v-card class="pa-4">
          <v-textarea v-model="text" outlined label="Enter your text" clearable />
          <v-btn color="primary" @click="generateChips">Submit</v-btn>
        </v-card>
        <v-card v-if="chips && chips.length" class="pa-4 mt-8">
          <div class="d-flex flex-wrap">
            <v-chip v-for="(item, i) in chips" :key="i" close class="ma-1" color="grey lighten-2" @click:close="removeWord(item)">
              {{ item.value }}
              <small class="ml-1 red--text font-weight-bold">({{item.count}})</small>
            </v-chip>
          </div>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "index",
  data() {
    return {
      text: 'Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry\'s standard and text of the printing and typesetting industry',
      chips: [],
    };
  },
  computed: {
    strings() {
      return this.text ? this.text.split(' ') : []
    }
  },
  methods: {
    generateChips() {
      const unique = [...new Set(this.strings)]
      this.chips = unique.map(item => ({ value: item, count : this.strings.filter(str => str === item).length}))
    },
    removeWord(word) {
      this.chips = this.chips.filter(item => item.value !== word.value)
      this.text = this.strings.filter(item => item !== word.value).join(' ')
    }
  }
}
</script>

<style scoped>

</style>