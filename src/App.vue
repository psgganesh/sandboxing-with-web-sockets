<template>
  <nav class="flex justify-start space-x-4 py-2 shadow-sm">
    <router-link
      to="/"
      class="font-medium px-3 py-2 text-slate-700 rounded-lg hover:bg-slate-100 hover:text-slate-900"
    >
      Home
    </router-link>
    <router-link
      to="/team"
      class="font-medium px-3 py-2 text-slate-700 rounded-lg hover:bg-slate-100 hover:text-slate-900"
    >
      Team
    </router-link>
  </nav>
  <router-view />
</template>
