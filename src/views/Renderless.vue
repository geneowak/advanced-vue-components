<template>
  <div id="app" class="bg-grey-lighter px-8 py-16 min-h-screen">
    <div class="max-w-sm w-full mx-auto">
      <tags-input v-model="tags"></tags-input>
    </div>

    <hr class="py-4 border-black" />

    <div class="max-w-sm w-full mx-auto">
      <renderless-tags-input v-model="tags">
        <div
          slot-scope="{ tags, removeTag, inputAttrs, inputEvents }"
          class="tags-input"
        >
          <span v-for="tag in tags" :key="tag" class="tags-input-tag">
            <span>{{ tag }}</span>
            <button
              type="button"
              class="tags-input-remove"
              @click="removeTag(tag)"
            >
              &times;
            </button>
          </span>
          <input
            type="text"
            class="tags-input-text"
            placeholder="Add tag..."
            v-bind="inputAttrs"
            v-on="inputEvents"
          />
        </div>
      </renderless-tags-input>
    </div>

    <hr class="py-4" />

    <div class="max-w-sm w-full mx-auto">
      <renderless-tags-input v-model="tags">
        <div
          slot-scope="{ tags, addTag, removeTag, inputAttrs, inputEvents }"
          class="p-4 rounded border bg-white"
        >
          <div class="flex">
            <input
              class="text-input flex-1 mr-2"
              placeholder="New tag"
              v-on="inputEvents"
              v-bind="inputAttrs"
            />
            <button type="button" class="btn btn-primary" @click="addTag">
              Add
            </button>
          </div>

          <ul v-show="tags.length > 0" class="mt-4 pl-6 text-left">
            <li v-for="tag in tags" class="mb-2" :key="tag">
              <span class="mr-2">{{ tag }}</span>
              <button
                class="text-grey-dark hover:text-grey-darkest underline text-sm"
                @click="removeTag(tag)"
              >
                Remove
              </button>
            </li>
          </ul>
        </div>
      </renderless-tags-input>
    </div>

    <hr class="py-4" />

    <inline-tags-input v-model="tags"></inline-tags-input>

    <hr class="py-4" />

    <fetch-vue-data></fetch-vue-data>
  </div>
</template>

<script>
import TagsInput from "@/components/renderless/TraditionalTagInputControl";
import RenderlessTagsInput from "@/components/renderless/RenderlessTagsInput";
import InlineTagsInput from "@/components/renderless/InlineTagsInput";
import FetchVueData from "@/components/renderless/FetchVueData";
export default {
  components: { TagsInput, RenderlessTagsInput, InlineTagsInput, FetchVueData },
  data() {
    return {
      tags: ["Testing", "Design"],
    };
  },
};
</script>

<style>
.tags-input {
  display: flex;
  flex-wrap: wrap;
  background-color: #fff;
  border-width: 1px;
  border-radius: 0.25rem;
  padding-left: 0.5rem;
  padding-right: 1rem;
  padding-top: 0.5rem;
  padding-bottom: 0.25rem;
}

.tags-input-tag {
  display: inline-flex;
  line-height: 1;
  align-items: center;
  font-size: 0.875rem;
  background-color: #bcdefa;
  color: #1c3d5a;
  border-radius: 0.25rem;
  user-select: none;
  padding: 0.25rem;
  margin-right: 0.5rem;
  margin-bottom: 0.25rem;
}

.tags-input-tag:last-of-type {
  margin-right: 0;
}

.tags-input-remove {
  color: #2779bd;
  font-size: 1.125rem;
  line-height: 1;
}

.tags-input-remove:first-child {
  margin-right: 0.25rem;
}

.tags-input-remove:last-child {
  margin-left: 0.25rem;
}

.tags-input-remove:focus {
  outline: 0;
}

.tags-input-text {
  flex: 1;
  outline: 0;
  padding-top: 0.25rem;
  padding-bottom: 0.25rem;
  margin-left: 0.5rem;
  margin-bottom: 0.25rem;
  min-width: 10rem;
}

.text-input {
  background-color: #fff;
  border-width: 1px;
  border-radius: 0.25rem;
  padding-left: 1rem;
  padding-right: 1rem;
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;
  width: 100%;
}

.text-input:focus {
  outline: 0;
}

.btn {
  font-weight: 600;
  border-radius: 0.25rem;
  padding-left: 1.5rem;
  padding-right: 1.5rem;
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;
}

.btn-primary {
  color: #fff;
  background-color: #6574cd;
}

.btn-primary:hover {
  background-color: #7886d7;
}

.py-16 {
  padding-top: 4rem;
  padding-bottom: 4rem;
}
</style>
