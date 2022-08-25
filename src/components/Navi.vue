<!--
  This example requires Tailwind CSS v2.0+ 
  
  This example requires some changes to your config:
  
  ```
  // tailwind.config.js
  module.exports = {
    // ...
    plugins: [
      // ...
      require('@tailwindcss/forms'),
    ],
  }
  ```
-->
<template>
  <Disclosure as="header" class="bg-white shadow" v-slot="{ open }">
    <div class="max-w-7xl mx-auto px-2 sm:px-4 lg:divide-y lg:divide-gray-200 lg:px-8">
      <div class="relative h-16 flex justify-between">
        <div class="relative z-10 px-2 flex lg:px-0">
          <div class="flex-shrink-0 flex items-center">
            <img class="block h-8 w-auto" src="https://tailwindui.com/img/logos/workflow-mark.svg?color=indigo&shade=600" alt="Workflow" />
          </div>
        </div>
        <div class="relative z-0 flex-1 px-2 flex items-center justify-center sm:absolute sm:inset-0">
          <div class="w-full sm:max-w-xs">
            <label for="search" class="sr-only">Search</label>
            <div class="relative">
              <div class="pointer-events-none absolute inset-y-0 left-0 pl-3 flex items-center">
                <SearchIcon class="h-5 w-5 text-gray-400" aria-hidden="true" />
              </div>
              <input id="search" name="search" class="block w-full bg-white border border-gray-300 rounded-md py-2 pl-10 pr-3 text-sm placeholder-gray-500 focus:outline-none focus:text-gray-900 focus:placeholder-gray-400 focus:ring-1 focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm" placeholder="Search" type="search" />
            </div>
          </div>
        </div>
        <div class="relative z-10 flex items-center lg:hidden">
          <!-- Mobile menu button -->
          <DisclosureButton class="rounded-md p-2 inline-flex items-center justify-center text-gray-400 hover:bg-gray-100 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-indigo-500">
            <span class="sr-only">Open menu</span>
            <MenuIcon v-if="!open" class="block h-6 w-6" aria-hidden="true" />
            <XIcon v-else class="block h-6 w-6" aria-hidden="true" />
          </DisclosureButton>
        </div>
        <div class="hidden lg:relative lg:z-10 lg:ml-4 lg:flex lg:items-center">
          <button type="button" class="flex-shrink-0 bg-white rounded-full p-1 text-gray-400 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
            <span class="sr-only">View notifications</span>
            <BellIcon class="h-6 w-6" aria-hidden="true" />
          </button>

          <!-- Profile dropdown -->
          <Menu as="div" class="flex-shrink-0 relative ml-4">
            <div>
              <MenuButton class="bg-white rounded-full flex focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                <span class="sr-only">Open user menu</span>
                <img class="h-8 w-8 rounded-full" :src="user.imageUrl" alt="" />
              </MenuButton>
            </div>
            <transition enter-active-class="transition ease-out duration-100" enter-from-class="transform opacity-0 scale-95" enter-to-class="transform opacity-100 scale-100" leave-active-class="transition ease-in duration-75" leave-from-class="transform opacity-100 scale-100" leave-to-class="transform opacity-0 scale-95">
              <MenuItems class="origin-top-right absolute right-0 mt-2 w-48 rounded-md shadow-lg bg-white ring-1 ring-black ring-opacity-5 py-1 focus:outline-none">
                <MenuItem v-for="item in userNavigation" :key="item.name" v-slot="{ active }">
                  <a :href="item.href" :class="[active ? 'bg-gray-100' : '', 'block py-2 px-4 text-sm text-gray-700']">{{ item.name }}</a>
                </MenuItem>
              </MenuItems>
            </transition>
          </Menu>
        </div>
      </div>
      <nav class="hidden lg:py-2 lg:flex lg:space-x-8" aria-label="Global">
        <a v-for="item in navigation" :key="item.name" :href="item.href" :class="[item.current ? 'bg-gray-100 text-gray-900' : 'text-gray-900 hover:bg-gray-50 hover:text-gray-900', 'rounded-md py-2 px-3 inline-flex items-center text-sm font-medium']" :aria-current="item.current ? 'page' : undefined">
          {{ item.name }}
        </a>
      </nav>
    </div>

    <DisclosurePanel as="nav" class="lg:hidden" aria-label="Global">
      <div class="pt-2 pb-3 px-2 space-y-1">
        <DisclosureButton v-for="item in navigation" :key="item.name" as="a" :href="item.href" :class="[item.current ? 'bg-gray-100 text-gray-900' : 'text-gray-900 hover:bg-gray-50 hover:text-gray-900', 'block rounded-md py-2 px-3 text-base font-medium']" :aria-current="item.current ? 'page' : undefined">{{ item.name }}</DisclosureButton>
      </div>
      <div class="border-t border-gray-200 pt-4 pb-3">
        <div class="px-4 flex items-center">
          <div class="flex-shrink-0">
            <img class="h-10 w-10 rounded-full" :src="user.imageUrl" alt="" />
          </div>
          <div class="ml-3">
            <div class="text-base font-medium text-gray-800">{{ user.name }}</div>
            <div class="text-sm font-medium text-gray-500">{{ user.email }}</div>
          </div>
          <button type="button" class="ml-auto flex-shrink-0 bg-white rounded-full p-1 text-gray-400 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
            <span class="sr-only">View notifications</span>
            <BellIcon class="h-6 w-6" aria-hidden="true" />
          </button>
        </div>
        <div class="mt-3 px-2 space-y-1">
          <DisclosureButton v-for="item in userNavigation" :key="item.name" as="a" :href="item.href" class="block rounded-md py-2 px-3 text-base font-medium text-gray-500 hover:bg-gray-50 hover:text-gray-900">{{ item.name }}</DisclosureButton>
        </div>
      </div>
    </DisclosurePanel>
  </Disclosure>

  <div class="leading-6 text-center text-black">
  <h1
    class="m-0 font-sans text-4xl font-extrabold tracking-tight leading-10 text-gray-900 xl:text-6xl sm:text-5xl sm:leading-none md:text-6xl md:leading-none"
  >
    Trending Tailwind templates
  </h1>
  <p
    class="mx-auto mt-3 mb-0 max-w-md text-base text-center text-gray-500 sm:text-lg sm:leading-7 md:mt-5 md:max-w-3xl md:text-xl md:leading-7"
  >
    Tailwind Awesome is a curated list of the best Tailwind templates &amp; UI
    kits in the internet. We are actively searching, and curating the coolest
    resources out there.
  </p>
  <div class="relative px-4 mx-auto mt-10 max-w-3xl text-center sm:px-6">
    <form action="/" accept-charset="UTF-8" method="get" class="text-black">
      <input
        value="all"
        autocomplete="off"
        type="hidden"
        name="price"
        id="price"
        class="p-0 m-0 cursor-default"
        style="font-size: 128%;"
      />
      <input
        value="template"
        autocomplete="off"
        type="hidden"
        name="type"
        id="type"
        class="p-0 m-0 cursor-default"
        style="font-size: 128%;"
      />
      <input
        value="any"
        autocomplete="off"
        type="hidden"
        name="technology"
        id="technology"
        class="p-0 m-0 cursor-default"
        style="font-size: 128%;"
      />
      <input
        value="trending"
        autocomplete="off"
        type="hidden"
        name="order"
        id="order"
        class="p-0 m-0 cursor-default"
        style="font-size: 128%;"
      />

      <div
        class="relative mx-auto w-full max-w-xl h-16 bg-white rounded-full lg:max-w-none"
      >
        <input
          placeholder="e.g. Blog"
          class="py-0 pr-32 pl-8 m-0 w-full h-16 text-base rounded-full border-2 border-gray-100 border-solid appearance-none cursor-text box-border outline-offset-2 focus:border-blue-600 focus:outline-offset-2"
          type="text"
          name="query"
          id="query"
          style="box-shadow: rgba(0, 0, 0, 0.05) 0px 0px 0px 1px; outline: transparent solid 2px;"
        />
        <button
          type="submit"
          class="inline-flex absolute top-3 right-3 items-center py-2 px-4 m-0 h-12 text-sm leading-5 text-white normal-case bg-indigo-800 bg-none rounded-full transition cursor-pointer sm:px-6 sm:text-base sm:font-medium sm:leading-6 outline-offset-2"
          style="outline: transparent solid 2px;"
        >
          <svg
            class="block mr-2 -ml-px w-4 h-4 font-medium align-middle sm:-ml-1 sm:h-5 sm:w-5"
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"
              class=""
            ></path>
          </svg>
          Search
        </button>
      </div>
    </form>
  </div>
</div>

<div class="py-12 tracking-normal leading-6 md:py-20 text-slate-800 bg-gray-200">
  <!-- Section header -->
  <div class="pb-12 mx-auto max-w-3xl leading-6 text-center">
    <h2
      class="mx-0 mt-0 mb-4 font-serif text-4xl font-bold leading-tight md:text-5xl md:tracking-normal"
    >
      Built exclusively for you
    </h2>
    <p class="m-0 text-xl leading-normal text-slate-500">
      Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia
      deserunt mollit anim id est laborum — semper quis lectus nulla at volutpat
      diam ut venenatis.
    </p>
  </div>

  <!-- Section content -->
  <div class="mx-auto max-w-3xl leading-6" x-data="{ tab: '1' }">
    <!-- Tabs buttons -->
    <div class="grid grid-cols-2 gap-6 pb-12 sm:grid-cols-4">
      <button
        class="p-0 m-0 text-center normal-case bg-transparent bg-none transition-opacity cursor-pointer"
        :class="tab === '1' || 'pv vs'"
        @click="tab = '1'"
        style="font-size: 128%;"
      >
        <div
          class="inline-flex mb-3 bg-white rounded-full"
          style="box-shadow: rgba(0, 0, 0, 0.05) 0px 0px 0px 1px;"
        >
          <svg
            width="56"
            height="56"
            xmlns="http://www.w3.org/2000/svg"
            class="block align-middle"
          >
            <path fill="#2174EA" d="M20 20h6v16h-6z" class=""></path>
            <path
              fill-opacity=".64"
              fill="#5091EE"
              d="M29 20h3v16h-3zM35 20h1v16h-1z"
              class=""
            ></path>
          </svg>
        </div>
        <div
          class="font-semibold leading-tight md:text-lg md:leading-normal md:tracking-normal"
        >
          Internal Feedback
        </div>
      </button>
      <button
        class="p-0 m-0 text-center normal-case bg-transparent bg-none opacity-50 transition-opacity cursor-pointer hover:opacity-75"
        :class="tab === '2' || 'pv vs'"
        @click="tab = '2'"
        style="font-size: 128%;"
      >
        <div
          class="inline-flex mb-3 bg-white rounded-full"
          style="box-shadow: rgba(0, 0, 0, 0.05) 0px 0px 0px 1px;"
        >
          <svg
            width="56"
            height="56"
            xmlns="http://www.w3.org/2000/svg"
            class="block align-middle"
          >
            <path
              fill-opacity=".64"
              fill="#5091EE"
              d="M33 23v8h3V20H25v3z"
              class=""
            ></path>
            <path fill="#2174EA" d="M20 25h11v11H20z" class=""></path>
          </svg>
        </div>
        <div
          class="font-semibold leading-tight md:text-lg md:leading-normal md:tracking-normal"
        >
          Internal Feedback
        </div>
      </button>
      <button
        class="p-0 m-0 text-center normal-case bg-transparent bg-none opacity-50 transition-opacity cursor-pointer hover:opacity-75"
        :class="tab === '3' || 'pv vs'"
        @click="tab = '3'"
        style="font-size: 128%;"
      >
        <div
          class="inline-flex mb-3 bg-white rounded-full"
          style="box-shadow: rgba(0, 0, 0, 0.05) 0px 0px 0px 1px;"
        >
          <svg
            width="56"
            height="56"
            xmlns="http://www.w3.org/2000/svg"
            class="block align-middle"
          >
            <path
              fill-opacity=".64"
              fill="#5091EE"
              d="M20 27l7-7h-7z"
              class=""
            ></path>
            <path fill="#2174EA" d="M29 20l7 7v-7z" class=""></path>
            <path
              fill-opacity=".64"
              fill="#5091EE"
              d="M36 29l-7 7h7z"
              class=""
            ></path>
            <path fill="#2174EA" d="M27 36l-7-7v7z" class=""></path>
          </svg>
        </div>
        <div
          class="font-semibold leading-tight md:text-lg md:leading-normal md:tracking-normal"
        >
          Internal Feedback
        </div>
      </button>
      <button
        class="p-0 m-0 text-center normal-case bg-transparent bg-none opacity-50 transition-opacity cursor-pointer hover:opacity-75"
        :class="tab === '4' || 'pv vs'"
        @click="tab = '4'"
        style="font-size: 128%;"
      >
        <div
          class="inline-flex mb-3 bg-white rounded-full"
          style="box-shadow: rgba(0, 0, 0, 0.05) 0px 0px 0px 1px;"
        >
          <svg
            width="56"
            height="56"
            xmlns="http://www.w3.org/2000/svg"
            class="block align-middle"
          >
            <path
              d="M24 28h-4v4.9c0 1 .7 1.9 1.7 2.1 1.2.2 2.3-.8 2.3-2v-5z"
              fill-opacity=".64"
              fill="#5091EE"
              class=""
            ></path>
            <path
              d="M35 21h-8c-.6 0-1 .4-1 1v11c0 .7-.2 1.4-.6 2H33c1.7 0 3-1.3 3-3V22c0-.6-.4-1-1-1z"
              fill="#2174EA"
              class=""
            ></path>
          </svg>
        </div>
        <div
          class="font-semibold leading-tight md:text-lg md:leading-normal md:tracking-normal"
        >
          Internal Feedback
        </div>
      </button>
    </div>

    <!-- Tab items -->
    <div
      class="flex relative flex-col opacity-100 duration-500 transform-none pointer-events-auto"
      data-aos="fade-up"
      style="transition-timing-function: cubic-bezier(0.25, 0.46, 0.45, 0.94); transition-property: opacity, transform, -webkit-transform;"
    >
      <div
        x-show="tab === '1'"
        x-transition:enter="p_ ds dn th"
        x-transition:enter-start="pc sw"
        x-transition:enter-end="ph sm"
        x-transition:leave="p_ ds di g"
        x-transition:leave-start="ph sm"
        x-transition:leave-end="pc sx"
        class="text-slate-800"
      >
        <img
          class="block mx-auto max-w-full h-auto align-middle"
          src="https://preview.cruip.com/tidy/images/features-home-01.jpg"
          width="768"
          height="474"
          alt="Features home 01"
          style="box-shadow: rgba(0, 0, 0, 0.05) 0px 0px 0px 1px;"
        />
      </div>
      <div
        x-show="tab === '2'"
        x-transition:enter="p_ ds dn th"
        x-transition:enter-start="pc sw"
        x-transition:enter-end="ph sm"
        x-transition:leave="p_ ds di g"
        x-transition:leave-start="ph sm"
        x-transition:leave-end="pc sx"
        style="display: none;"
        class="hidden text-slate-800"
      >
        <img
          class="block mx-auto max-w-full h-auto align-middle"
          src="https://preview.cruip.com/tidy/images/features-home-01.jpg"
          width="768"
          height="474"
          alt="Features home 02"
          style="box-shadow: rgba(0, 0, 0, 0.05) 0px 0px 0px 1px;"
        />
      </div>
      <div
        x-show="tab === '3'"
        x-transition:enter="p_ ds dn th"
        x-transition:enter-start="pc sw"
        x-transition:enter-end="ph sm"
        x-transition:leave="p_ ds di g"
        x-transition:leave-start="ph sm"
        x-transition:leave-end="pc sx"
        style="display: none;"
        class="hidden text-slate-800"
      >
        <img
          class="block mx-auto max-w-full h-auto align-middle"
          src="https://preview.cruip.com/tidy/images/features-home-01.jpg"
          width="768"
          height="474"
          alt="Features home 03"
          style="box-shadow: rgba(0, 0, 0, 0.05) 0px 0px 0px 1px;"
        />
      </div>
      <div
        x-show="tab === '4'"
        x-transition:enter="p_ ds dn th"
        x-transition:enter-start="pc sw"
        x-transition:enter-end="ph sm"
        x-transition:leave="p_ ds di g"
        x-transition:leave-start="ph sm"
        x-transition:leave-end="pc sx"
        style="display: none;"
        class="hidden text-slate-800"
      >
        <img
          class="block mx-auto max-w-full h-auto align-middle"
          src="https://preview.cruip.com/tidy/images/features-home-01.jpg"
          width="768"
          height="474"
          alt="Features home 04"
          style="box-shadow: rgba(0, 0, 0, 0.05) 0px 0px 0px 1px;"
        />
      </div>
    </div>
  </div>
</div>

</template>

<script setup>
import { Disclosure, DisclosureButton, DisclosurePanel, Menu, MenuButton, MenuItem, MenuItems } from '@headlessui/vue'
import { SearchIcon } from '@heroicons/vue/solid'
import { BellIcon, MenuIcon, XIcon } from '@heroicons/vue/outline'

const user = {
  name: 'Tom Cook',
  email: 'tom@example.com',
  imageUrl:
    'https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
}
const navigation = [
  { name: 'Dashboard', href: '#', current: true },
  { name: 'Team', href: '#', current: false },
  { name: 'Projects', href: '#', current: false },
  { name: 'Calendar', href: '#', current: false },
]
const userNavigation = [
  { name: 'Your Profile', href: '#' },
  { name: 'Settings', href: '#' },
  { name: 'Sign out', href: '#' },
]
</script>






