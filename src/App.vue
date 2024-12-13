<script setup>
import { ref } from 'vue'
import { Dialog, DialogPanel } from '@headlessui/vue'
import { Bars3Icon, XMarkIcon } from '@heroicons/vue/24/outline'

const mobileMenuOpen = ref(false)

const navigation = [
  { name: 'Sites', href: '#' },
  { name: 'Pages', href: '#' },
  { name: 'Modules', href: '#' },
  { name: 'Logs', href: '#' },
  { name: 'System-Info', href: '#' },
]

const sites = ref(null)
var headers = {
  'content-type': 'application/json',
  'Authorization': 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1bmlxdWVfbmFtZSI6ImFkbWluQG14cG9jLmNvbSIsIm5hbWVpZCI6IjEiLCJPcXRhbmUuSWRlbnRpdHkuU2l0ZUtleSI6IjE6MSIsInJvbGUiOlsiSG9zdCBVc2VycyIsIkFkbWluaXN0cmF0b3JzIiwiUmVnaXN0ZXJlZCBVc2VycyJdLCJBc3BOZXQuSWRlbnRpdHkuU2VjdXJpdHlTdGFtcCI6IlNLQkJIU0JFTlFMUFhaQURMUUpYVlhORlVZTzdWN1RGIiwibmJmIjoxNzM0MDA5NzY4LCJleHAiOjE3NjU1NDU3NjgsImlhdCI6MTczNDAwOTc2OCwiaXNzIjoiaHR0cDovL2xvY2FsaG9zdDo0NDM1NyIsImF1ZCI6Imh0dHA6Ly9sb2NhbGhvc3Q6NTE3MyJ9.0EC8IqhDYSAxnshzUOA7BD2hfCrMzdFCu2eiRDXRMHs'
};
fetch('http://localhost:44357/api/Site',
  headers)
  .then(response => response.json())
  .then(data => sites.value = data)
  .catch(err => console.error(err));

</script>

<template>
  <div class="bg-white">
    <header class="absolute inset-x-0 top-0 z-50">
      <nav class="flex items-center justify-between p-6 lg:px-8" aria-label="Global">
        <div class="flex lg:flex-1">
          <a href="#" class="-m-1.5 p-1.5">
            <span class="sr-only">Welcome to Oqtane Saas</span>
            <img class="h-8 w-auto" src="https://tailwindui.com/plus/img/logos/mark.svg?color=indigo&shade=600"
              alt="" />
          </a>
        </div>
        <div class="flex lg:hidden">
          <button type="button" class="-m-2.5 inline-flex items-center justify-center rounded-md p-2.5 text-gray-700"
            @click="mobileMenuOpen = true">
            <span class="sr-only">Open main menu</span>
            <Bars3Icon class="size-6" aria-hidden="true" />
          </button>
        </div>
        <div class="hidden lg:flex lg:gap-x-12">
          <a v-for="item in navigation" :key="item.name" :href="item.href"
            class="text-sm/6 font-semibold text-gray-900">{{ item.name }}</a>
        </div>
        <div class="hidden lg:flex lg:flex-1 lg:justify-end">
          <a href="#" class="text-sm/6 font-semibold text-gray-900">Log in <span aria-hidden="true">&rarr;</span></a>
        </div>
      </nav>
      <Dialog class="lg:hidden" @close="mobileMenuOpen = false" :open="mobileMenuOpen">
        <div class="fixed inset-0 z-50" />
        <DialogPanel
          class="fixed inset-y-0 right-0 z-50 w-full overflow-y-auto bg-white px-6 py-6 sm:max-w-sm sm:ring-1 sm:ring-gray-900/10">
          <div class="flex items-center justify-between">
            <a href="#" class="-m-1.5 p-1.5">
              <span class="sr-only">Your Company</span>
              <img class="h-8 w-auto" src="https://tailwindui.com/plus/img/logos/mark.svg?color=indigo&shade=600"
                alt="" />
            </a>
            <button type="button" class="-m-2.5 rounded-md p-2.5 text-gray-700" @click="mobileMenuOpen = false">
              <span class="sr-only">Close menu</span>
              <XMarkIcon class="size-6" aria-hidden="true" />
            </button>
          </div>
          <div class="mt-6 flow-root">
            <div class="-my-6 divide-y divide-gray-500/10">
              <div class="space-y-2 py-6">
                <a v-for="item in navigation" :key="item.name" :href="item.href"
                  class="-mx-3 block rounded-lg px-3 py-2 text-base/7 font-semibold text-gray-900 hover:bg-gray-50">{{
                    item.name }}</a>
              </div>
              <div class="py-6">
                <a href="#"
                  class="-mx-3 block rounded-lg px-3 py-2.5 text-base/7 font-semibold text-gray-900 hover:bg-gray-50">Log
                  in</a>
              </div>
            </div>
          </div>
        </DialogPanel>
      </Dialog>
    </header>

    <ul v-for="site in sites">
      <li>{{ site }}</li>
    </ul>

    <div class="bg-white py-24 sm:py-32">
      <div class="mx-auto max-w-7xl px-6 lg:px-8">
        <div class="mx-auto max-w-2xl lg:mx-0">
          <h2 class="text-pretty text-4xl font-semibold tracking-tight text-gray-900 sm:text-5xl">Welcome to Oqtane Saas</h2>
          <p class="mt-2 text-lg/8 text-gray-600">Manage Oqtane objects</p>
        </div>
        <div
          class="mx-auto mt-10 grid max-w-2xl grid-cols-1 gap-x-8 gap-y-16 border-t border-gray-200 pt-10 sm:mt-16 sm:pt-16 lg:mx-0 lg:max-w-none lg:grid-cols-3">
          <article class="flex max-w-xl flex-col items-start justify-between">
            <div class="flex items-center gap-x-4 text-xs">
              <time datetime="2020-03-16" class="text-gray-500">Nov 16, 2024</time>
              <a href="#"
                class="relative z-10 rounded-full bg-gray-50 px-3 py-1.5 font-medium text-gray-600 hover:bg-gray-100">Sites</a>
            </div>
            <div class="group relative">
              <h3 class="mt-3 text-lg/6 font-semibold text-gray-900 group-hover:text-gray-600">
                <a href="#">
                  <span class="absolute inset-0"></span>
                  Site updated
                </a>
              </h3>
              <p class="mt-5 line-clamp-3 text-sm/6 text-gray-600">Info- New site added to the queue</p>
            </div>
            <div class="relative mt-8 flex items-center gap-x-4">
              <img
                src="https://images.unsplash.com/"
                alt="" class="size-10 rounded-full bg-gray-50">
              <div class="text-sm/6">
                <p class="font-semibold text-gray-900">
                  <a href="#">
                    <span class="absolute inset-0"></span>
                    By- Sufiyan Budye
                  </a>
                </p>
                <p class="text-gray-600">Developer</p>
              </div>
            </div>
          </article>

          <!-- More posts... -->
        </div>
      </div>
    </div>
  </div>
</template>
