<template>
  <AppForm>
    <h4>Editor</h4>
    <AppFormItem label="Tab size">
      <AppInput v-model="tabSize" />
      <div class="desc">
        The number of spaces a tab is equal to.
      </div>
    </AppFormItem>
    <AppFormItem label="Indent using">
      <AppSelect
        v-model="insertSpaces"
        :options="insertSpacesOptions"
      />
      <div class="desc">
        Select type of indentation.
      </div>
    </AppFormItem>
    <AppFormItem label="Whitespace">
      <AppSelect
        v-model="renderWhitespace"
        :options="renderWhitespaceOptions"
      />
      <div class="desc">
        Controls how the editor should render whitespace characters.
      </div>
    </AppFormItem>
    <AppFormItem label="Word wrapping">
      <AppSelect
        v-model="wordWrap"
        :options="wordWrapOptions"
      />
      <div class="desc">
        Controls how lines should wrap.
      </div>
    </AppFormItem>
    <h4>Format</h4>
    <AppFormItem label="Semicolons">
      <AppCheckbox v-model="prettierSemi">
        Enable
      </AppCheckbox>
      <div class="desc">
        Print semicolons at the ends of statements.
      </div>
    </AppFormItem>
    <AppFormItem label="Single Quotes">
      <AppCheckbox v-model="prettierQuotes">
        Enable
      </AppCheckbox>
      <div class="desc">
        Use single quotes instead of double quotes.
      </div>
    </AppFormItem>
  </AppForm>
</template>

<script>
import { mapState } from 'vuex'

export default {
  name: 'Editor',

  data () {
    return {
      renderWhitespaceOptions: [
        { label: 'None', value: 'none' },
        { label: 'Boundary', value: 'boundary' },
        { label: 'All', value: 'all' }
      ],
      wordWrapOptions: [
        { label: 'Off', value: 'off' },
        { label: 'On', value: 'on' },
        { label: 'Column', value: 'wordWrapColumn' }
      ],
      insertSpacesOptions: [
        { label: 'Spaces', value: true },
        { label: 'Tabs', value: false }
      ]
    }
  },

  computed: {
    ...mapState(['preferences']),
    renderWhitespace: {
      get () {
        return this.preferences.renderWhitespace
      },
      set (v) {
        this.$store.dispatch('preferences/setWhitespaceType', v)
      }
    },
    wordWrap: {
      get () {
        return this.preferences.wordWrap
      },
      set (v) {
        this.$store.dispatch('preferences/setWordWrap', v)
      }
    },
    tabSize: {
      get () {
        return this.preferences.tabSize
      },
      set (v) {
        this.$store.dispatch('preferences/setTabSize', v)
      }
    },
    insertSpaces: {
      get () {
        return this.preferences.insertSpaces
      },
      set (v) {
        this.$store.dispatch('preferences/setInsertSpaces', JSON.parse(v))
      }
    },
    prettierSemi: {
      get () {
        return this.preferences.prettierSemi
      },
      set (v) {
        this.$store.dispatch('preferences/setPrettierSemi', v)
      }
    },
    prettierQuotes: {
      get () {
        return this.preferences.prettierQuotes
      },
      set (v) {
        this.$store.dispatch('preferences/setPrettierQuotes', v)
      }
    }
  }
}
</script>

<style lang="scss">
h4 {
  &:first-of-type {
    margin-top: 0;
  }
}
</style>
