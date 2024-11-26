<template>
  <!-- Palette -->
  <div class="flex flex-col gap-3 container w-7/12">
    <!-- Header -->
    <div class="flex flex-row gap-2 items-center justify-between px-2">
      <!-- Title -->
      <h1
        v-motion
        :initial="{ opacity: 0, y: 40 }"
        :visible-once="{
          y: 0,
          opacity: 1,
        }"
        class="text-lg font-light text-center"
      >
        {{ props.colorName.name }}
      </h1>

      <!-- Right -->
      <div class="flex flex-row gap-2 items-center">
        <AlertDialog>
          <AlertDialogTrigger as-child>
            <button
              class="dark:text-zinc-400 dark:hover:text-zinc-300 transition-all duration-200 ease-in-out"
              @click="onExportClick()"
            >
              Export
            </button>
          </AlertDialogTrigger>
          <AlertDialogContent>
            <AlertDialogHeader>
              <AlertDialogTitle>Are you absolutely sure?</AlertDialogTitle>
              <AlertDialogDescription>
                This action cannot be undone. This will permanently delete your
                account and remove your data from our servers.
              </AlertDialogDescription>
            </AlertDialogHeader>
            <AlertDialogFooter>
              <AlertDialogCancel>Cancel</AlertDialogCancel>
              <AlertDialogAction>Continue</AlertDialogAction>
            </AlertDialogFooter>
          </AlertDialogContent>
        </AlertDialog>
      </div>
    </div>

    <!-- Color Palette -->
    <div
      class="flex flex-row flex-wrap gap-3 justify-center text-xs"
      v-if="props.colorPalette.length > 0"
    >
      <template v-for="paletteColor in props.colorPalette">
        <ColorButton
          :paletteColor="paletteColor"
          :themeVariableKey="props.themeVariableKey"
        />
      </template>
    </div>
  </div>
</template>

<script setup lang="ts">
  // features
  import ColorButton from '@/components/features/ColorButton.vue';

  // models
  import { IPaletteColor } from '@/shared/models/color.model';

  // shadcn
  import {
    AlertDialog,
    AlertDialogAction,
    AlertDialogCancel,
    AlertDialogContent,
    AlertDialogDescription,
    AlertDialogFooter,
    AlertDialogHeader,
    AlertDialogTitle,
    AlertDialogTrigger,
  } from '@/components/ui/alert-dialog';

  const props = defineProps<{
    colorPalette: IPaletteColor[];
    colorName: any;
    themeVariableKey: ColorVariableTheme;
  }>();
</script>
