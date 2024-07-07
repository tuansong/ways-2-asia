<script lang="ts" setup>
const { data: navigation } = await useAsyncData('navigation', () => fetchContentNavigation())
const { data: files } = useLazyFetch('/api/search.json', { default: () => [], server: false })

const links = [
  {
    label: 'Vietnã',
    to: '/categories/vietnam',
  },
  {
    label: 'Indonésia',
    to: '/categories/environmental-impacts',
  },
  {
    label: 'Tailândia',
    to: '/categories/sustainable-practices',
  },
  {
    label: 'Malásia',
    to: '/categories/customer-stories',
  },
  {
    label: 'Others',
    to: '/categories/behind-the-scenes',
  },
]

const footerLinks = [
  {
    label: 'Produtos',
    children: [
      {
        label: 'Características',
        to: '#',
      },
      {
        label: 'Preços',
        to: '#',
      },
      {
        label: 'Integrações',
        to: '#',
      },
      {
        label: 'Segurança',
        to: '#',
      },
    ],
  },
  {
    label: 'Comprar',
    children: [
      {
        label: 'Acessórias',
        to: '#',
      },
      {
        label: 'Presentes',
        to: '#',
      },
    ],
  },
  {
    label: 'Empresa',
    children: [
      {
        label: 'Sobre',
        to: '#',
      },
      {
        label: 'Blogue',
        to: '#',
      },
      {
        label: 'Carreiras',
        to: '#',
      },
    ],
  },
]

const { toggleContentSearch } = useUIState()
const { metaSymbol } = useShortcuts()
</script>

<template>
  <UHeader
    :links="links"
  >
    <template #logo>
      Ways2Asia
    </template>

    <template #right>
      <UTooltip
        text="Search"
        :shortcuts="[metaSymbol, 'k']"
      >
        <UButton
          icon="i-heroicons-magnifying-glass-solid"
          variant="ghost"
          color="gray"
          @click="toggleContentSearch"
        >
          <span class="sr-only">Search</span>
        </UButton>
      </UTooltip>
      <FollowUs />
    </template>
  </UHeader>

  <UMain>
    <NuxtPage />
  </UMain>

  <UFooter class="mt-24">
    <template #top>
      <div class="grid grid-cols-1 xl:grid-cols-2 gap-12 xl:gap-0">
        <span class="text-xl font-bold">
          Ways2Asia
        </span>

        <ol class="xl:place-self-end grid grid-cols-2 md:grid-cols-3 gap-8 xl:gap-20">
          <li
            v-for="item in footerLinks"
            :key="item.label"
          >
            <span class="font-semibold">
              {{ item.label }}
            </span>
            <ol class="mt-3 flex flex-col text-zinc-700">
              <li
                v-for="child in item.children"
                :key="child.label"
              >
                <ULink
                  :to="child.to"
                  class="block py-1 hover:underline hover:underline-offset-2"
                >
                  {{ child.label }}
                </ULink>
              </li>
            </ol>
          </li>
        </ol>
      </div>
    </template>
    <template #left>
      <div class="flex flex-col md:flex-row items-center gap-4">
        <span class="text-sm text-stone-500">
          © 2024 Ways2Asia. All rights reserved.
        </span>
        <div class="flex gap-2 text-xs text-stone-500">
          <ULink to="#">
            política de Privacidade
          </ULink>
          <ULink to="#">
            Termos de serviço
          </ULink>
        </div>
      </div>
    </template>
    <template #right>
      <FollowUs />
    </template>
  </UFooter>

  <ClientOnly>
    <LazyUDocsSearch
      :files="files"
      :links="links"
      :navigation="navigation"
    />
  </ClientOnly>
</template>
