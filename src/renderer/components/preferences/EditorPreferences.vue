<template>
  <div class="editor-preferences">
    <AppForm>
      <h4>{{ i18n.t('preferences:editor.label') }}</h4>
      <AppFormItem :label="i18n.t('preferences:editor.fontSize')">
        <AppInput
          v-model="appStore.editor.fontSize"
          type="number"
          style="width: 100px"
        />
      </AppFormItem>
      <AppFormItem :label="i18n.t('preferences:editor.fontFamily')">
        <AppInput v-model="appStore.editor.fontFamily" />
      </AppFormItem>
      <AppFormItem :label="i18n.t('preferences:editor.wrap.label')">
        <AppSelect
          v-model="appStore.editor.wrap"
          :options="wrapOptions"
        />
      </AppFormItem>
      <AppFormItem :label="i18n.t('preferences:editor.tabSize')">
        <AppInput
          v-model="appStore.editor.tabSize"
          type="number"
          style="width: 100px"
        />
      </AppFormItem>
      <AppFormItem :label="i18n.t('preferences:editor.showInvisibles')">
        <AppCheckbox
          v-model="appStore.editor.showInvisibles"
          name="showInvisibles"
        />
      </AppFormItem>
      <AppFormItem :label="i18n.t('preferences:editor.highlightLine')">
        <AppCheckbox
          v-model="appStore.editor.highlightLine"
          name="highlightLine"
        />
      </AppFormItem>
      <AppFormItem :label="i18n.t('preferences:editor.highlightGutter')">
        <AppCheckbox
          v-model="appStore.editor.highlightGutter"
          name="highlightGutter"
        />
      </AppFormItem>
      <h4>{{ i18n.t('preferences:editor.prettier.label') }}</h4>
      <AppFormItem
        :label="i18n.t('preferences:editor.prettier.trailingComma.label')"
      >
        <AppSelect
          v-model="appStore.editor.trailingComma"
          :options="trailingCommaOptions"
        />
      </AppFormItem>
      <AppFormItem :label="i18n.t('preferences:editor.prettier.semi')">
        <AppCheckbox
          v-model="appStore.editor.semi"
          name="semi"
        />
      </AppFormItem>
      <AppFormItem :label="i18n.t('preferences:editor.prettier.singleQuote')">
        <AppCheckbox
          v-model="appStore.editor.singleQuote"
          name="singleQuote"
        />
      </AppFormItem>
    </AppForm>
  </div>
</template>

<script setup lang="ts">
import { store, i18n } from '@/electron'
import { useAppStore } from '@/store/app'
import { watch } from 'vue'

const appStore = useAppStore()

const wrapOptions = [
  { label: i18n.t('preferences:editor.wrap.wordWrap'), value: 'free' },
  { label: i18n.t('preferences:editor.wrap.off'), value: 'off' }
]

const trailingCommaOptions = [
  {
    label: i18n.t('preferences:editor.prettier.trailingComma.none'),
    value: 'none'
  },
  {
    label: i18n.t('preferences:editor.prettier.trailingComma.all'),
    value: 'all'
  },
  {
    label: i18n.t('preferences:editor.prettier.trailingComma.es6'),
    value: 'es6'
  }
]

watch(
  () => appStore.editor,
  v => {
    store.preferences.set('editor', { ...v })
  },
  { deep: true }
)
</script>

<style lang="scss" scoped>
h4 {
  &:first-child {
    margin-top: 0;
  }
  margin-bottom: 0;
}
</style>
