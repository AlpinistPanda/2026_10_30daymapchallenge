<template>
  <footer
    class="bg-[#ff0000] absolute bottom-0 left-0 w-full flex items-center justify-between px-6 py-3 text-sm text-white z-20"
  >
    <!-- Left: logos -->
    <div class="flex items-center gap-4">

      <img
        src="/img/logo.png"
        alt="Coding Café"
        class="h-8 object-contain"
      />
    </div>

    <!-- Center: title -->
    <div class="text-center font-medium tracking-wide">
      BE Coding Café - 28 October 2026
    </div>

    <!-- Right: slide numbers -->
    <div class="text-right tabular-nums">
      {{ $slidev.nav.currentPage }} / {{ $slidev.nav.total }}
    </div>
  </footer>
</template>
