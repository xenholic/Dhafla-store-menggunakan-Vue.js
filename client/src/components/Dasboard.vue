<script>
export default {
  name: "Dashboard",
  props: ["user"],
};
</script>
<template>
  <!-- Start dashboard -->
  <div class="container mx-auto px-4 sm:px-8 max-w-full">
    <div class="py-8">
      <div class="-mx-4 sm:-mx-8 px-4 sm:px-8 py-4 overflow-x-auto">
        <div
          class="inline-block min-w-full shadow rounded-lg overflow-hidden w-full p-8 my-2"
        >
          <p class="text-2xl mb-3">Welcome DHafla</p>
          <span class="text-muted text-xs">Find your Passion Here! </span>
        </div>
        <figure class="bg-slate-100 rounded-xl p-8 dark:bg-slate-800">
          <img
            class="w-24 h-24 rounded-full mx-auto"
            src="https://media.suara.com/pictures/970x544/2022/03/22/20973-potret-anime-your-name-instagramcommakotoshinkai.jpg"
            alt=""
            width="384"
            height="512"
          />
          <div class="pt-6 space-y-4">
            <blockquote>
              <p class="text-lg font-medium">
                “Ini tailwind ada yang nyomot ada yang otak atik sendiri, semoga
                bisa menambah ilmu dan nilai.”
              </p>
            </blockquote>
            <figcaption class="font-medium">
              <div class="text-sky-500 dark:text-sky-400">
                {{ user.username }}
              </div>
              <div class="text-slate-700 dark:text-slate-500">
                {{ user.email }}
              </div>
            </figcaption>
          </div>
        </figure>
      </div>
    </div>
  </div>
  <!-- End dashboard-->
</template>

<style></style>
