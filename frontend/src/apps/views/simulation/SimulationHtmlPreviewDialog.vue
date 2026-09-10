<script setup lang="ts">
import { useI18n } from "vue-i18n";
import { VustButton, VustDialog } from "@/components/ui";

defineProps<{
  visible: boolean;
  html: string;
}>();

const emit = defineEmits<{
  close: [];
}>();

const { t } = useI18n();
</script>

<template>
  <VustDialog
    :visible="visible"
    :title="t('app.simulation.rules.preview.title')"
    width="min(1080px, 94vw)"
    data-ui="simulation-html-preview-dialog"
    @close="emit('close')"
  >
    <div class="html-preview-shell" data-slot="body">
      <iframe
        :srcdoc="html"
        class="html-preview-frame"
        sandbox=""
        referrerpolicy="no-referrer"
        data-slot="preview-frame"
      ></iframe>
    </div>

    <template #footer>
      <VustButton
        type="secondary"
        data-ui="simulation-html-preview-close"
        @click="emit('close')"
      >
        {{ t("app.simulation.rules.preview.close") }}
      </VustButton>
    </template>
  </VustDialog>
</template>

<style scoped>
.html-preview-shell {
  height: clamp(320px, 62vh, 680px);
  overflow: hidden;
  border: 1px solid var(--vdl-border-subtle);
  border-radius: var(--vdl-radius-md);
  background-color: #ffffff;
}

.html-preview-frame {
  display: block;
  width: 100%;
  height: 100%;
  border: 0;
  background-color: #ffffff;
}
</style>
