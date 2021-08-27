<template>
  <renderless-tags-input
    :value="value"
    @input="
      (tags) => {
        $emit('input', tags);
      }
    "
  >
    <div
      class="tags-input"
      slot-scope="{ tag, removeTag, inputAttrs, inputEvents }"
    >
      <span class="tags-input-tag" v-for="tag in value" :key="tag">
        <span>{{ tag }}</span>
        <button type="button" @click="removeTag(tag)" class="tags-input-remove">
          &times;
        </button>
      </span>
      <input
        type="text"
        class="tags-input-text"
        v-bind="inputAttrs"
        v-on="inputEvents"
        placeholder="Add tag..."
      />
    </div>
  </renderless-tags-input>
</template>

<script>
import RenderlessTagsInput from "./RenderlessTagsInput";
export default {
  props: ["value"],
  components: { RenderlessTagsInput },
};
</script>
