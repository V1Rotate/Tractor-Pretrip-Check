<template>
  <header>
    <div class="flex text-md justify-evenly items-center mb-4">
      <h2 class="tracking-wide subpixel-antialiased font-medium text-amber-800">
        {{ truckModel }}
      </h2>
      <a
        href="https://dtnacontent-dtna.prd.freightliner.com/content/public/dtna-servicelit/dtna/en_us/freightliner/drivers-manuals/new-cascadia-drivers-manual.html?SM_USER="
        target="blank"
        class="manual"
        ><h4
          class="bg-[#af954d] text-white text-xs rounded-md p-0.5 pl-1 pr-1 motion-safe:animate-pulse hover:scale-105 duration-300"
        >
          Driver's Manual
        </h4></a
      >
      <!--Official Freightliner Cascadia Open Source Driver's Manual-->
    </div>
    <div
      class="flex justify-center text-red-600 mb-8 tracking-widest font-semibold"
    >
      <h4>{{ appName }}</h4>
    </div>
  </header>
</template>

<script>
export default {
  name: 'Header',
  //Application can be developed for the Volvo VNL, the secondly most ofter truck model used in the Bison Transport Fleet, based on my research.
  props: {
    truckModel: String,
    appName: String,
  },
};
</script>
