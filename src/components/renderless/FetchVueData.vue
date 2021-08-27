<template>
  <div id="app" class="min-h-screen font-sans bg-grey-lighter">
    <div class="container mx-auto max-w-md p-6">
      <fetch-data url="https://api.github.com/orgs/vuejs/repos">
        <div slot-scope="{ loading, response: repos }">
          <div v-if="loading">Loading repositories...</div>
          <div v-else>
            <div
              v-for="repo in repos"
              :key="repo.id"
              class="shadow-md bg-white p-6 mb-6 rounded"
            >
              <div class="flex mb-4">
                <a :href="repo.html_url" class="text-blue no-underline"
                  ><h2 class="text-lg mr-4">{{ repo.full_name }}</h2></a
                >
                <div class="flex items-center">
                  <svg
                    class="fill-current text-grey-dark h-3 w-3 mr-1"
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 20 20"
                  >
                    <path
                      d="M10 15l-5.878 3.09 1.123-6.545L.489 6.91l6.572-.955L10 0l2.939 5.955 6.572.955-4.756 4.635 1.123 6.545z"
                    />
                  </svg>
                  <span class="text-grey-darker text-sm">{{
                    repo.stargazers_count
                  }}</span>
                </div>
              </div>
              <div>
                <h3 class="text-base text-grey-darker font-medium mb-2">
                  Top Contributors
                </h3>
                <fetch-data :url="repo.contributors_url">
                  <div slot-scope="{ loading, response: contributors }">
                    <div v-if="loading">Loading contributors...</div>

                    <div v-else>
                      <div
                        v-for="contributor in contributors.slice(0, 5)"
                        :key="contributor.id"
                        class="inline-flex items-center mr-6"
                      >
                        <span class="mr-1">
                          <img
                            :src="contributor.avatar_url"
                            class="h-6 w-6 rounded-full"
                            alt=""
                          />
                        </span>
                        <a
                          :href="contributor.html_url"
                          class="text-sm text-grey-dark font-medium"
                          >{{ contributor.login }}</a
                        >
                      </div>
                    </div>
                  </div>
                </fetch-data>
              </div>
            </div>
          </div>
        </div>
      </fetch-data>
    </div>
  </div>
</template>

<script>
import FetchData from "./RenderlessFetchData";
export default {
  components: { FetchData },
};
</script>
