<template>
    <div>

    <div @click="setIsClose" :class="isOpen ? 'overlay open' : 'overlay'"></div>
      
    <button @click="setIsOpen" class="sidebar-btn">
      <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" aria-hidden="true" role="img" width="35" height="35" preserveAspectRatio="xMidYMid meet" viewBox="0 0 24 24"><g><circle cx="4" cy="12" r="1"></circle><rect x="7" y="11" width="14" height="2" rx=".94" ry=".94"></rect><rect x="3" y="16" width="18" height="2" rx=".94" ry=".94"></rect><rect x="3" y="6" width="18" height="2" rx=".94" ry=".94"></rect></g>
      </svg>
    </button>
    
    <aside :class="isOpen ? 'sidebar open' : 'sidebar'">
      <a href="#" class="logo">
        <img class="logo__img" src="https://res.cloudinary.com/dexg5uy3d/image/upload/v1636509322/1623361712889_fwycjx.jpg" alt="">
      </a>
      <div class="user">
        <a href="#" class="user__link">
          <img src="https://res.cloudinary.com/dexg5uy3d/image/upload/v1636510243/1623366660297_sauxl0.jpg" class="user__img" alt="">
          <p class="user__name">Sean Filimon</p>
        </a>
      </div>
      <ul class="menu">
        <li @click="onClick(index)" v-for="(item, index) in list" :key="item" :class="index === active ? 'menu__list active' : 'menu__list'">
          <a href="#" class="menu__link">
            <div v-html="item.svg"></div>
            <div class="menu__title">{{item.name}}</div>
          </a>
        </li>
      </ul>
    </aside>
    </div>
</template>

<script>
export default {
  name: 'Sidebar',
  props: ['toggle'],
  data() {
    return {
      list: [
        {
          svg: `<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" aria-hidden="true" role="img" width="22" height="22" preserveAspectRatio="xMidYMid meet" viewBox="0 0 24 24"><g><path d="M14.5 10.33h6.67A.83.83 0 0 0 22 9.5A7.5 7.5 0 0 0 14.5 2a.83.83 0 0 0-.83.83V9.5a.83.83 0 0 0 .83.83zm.83-6.6a5.83 5.83 0 0 1 4.94 4.94h-4.94z"></path><path d="M21.08 12h-8.15a.91.91 0 0 1-.91-.91V2.92A.92.92 0 0 0 11 2a10 10 0 1 0 11 11a.92.92 0 0 0-.92-1z"></path></g></svg>`,
          name: 'Dashboard'
        },
        {
          svg: `<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" aria-hidden="true" role="img" width="22" height="22" preserveAspectRatio="xMidYMid meet" viewBox="0 0 24 24"><path d="M9 11a4 4 0 1 0-4-4a4 4 0 0 0 4 4zm8 2a3 3 0 1 0-3-3a3 3 0 0 0 3 3zm4 7a1 1 0 0 0 1-1a5 5 0 0 0-8.06-3.95A7 7 0 0 0 2 20a1 1 0 0 0 1 1h12a1 1 0 0 0 1-1"></path></svg>`,
          name: 'Profile'
        },
        {
          svg: `<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" aria-hidden="true" role="img" width="22" height="22" preserveAspectRatio="xMidYMid meet" viewBox="0 0 24 24"><path d="M19.74 7.33l-4.44-5a1 1 0 0 0-.74-.33h-8A2.53 2.53 0 0 0 4 4.5v15A2.53 2.53 0 0 0 6.56 22h10.88A2.53 2.53 0 0 0 20 19.5V8a1 1 0 0 0-.26-.67zM9 12h3a1 1 0 0 1 0 2H9a1 1 0 0 1 0-2zm6 6H9a1 1 0 0 1 0-2h6a1 1 0 0 1 0 2zm-.29-10a.79.79 0 0 1-.71-.85V4l3.74 4z"></path></svg>`,
          name: 'Files'
        },
        {
          svg: `<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" aria-hidden="true" role="img" width="22" height="22" preserveAspectRatio="xMidYMid meet" viewBox="0 0 24 24"><g ><path d="M21.08 7a2 2 0 0 0-1.7-1H6.58L6 3.74A1 1 0 0 0 5 3H3a1 1 0 0 0 0 2h1.24L7 15.26A1 1 0 0 0 8 16h9a1 1 0 0 0 .89-.55l3.28-6.56A2 2 0 0 0 21.08 7z"></path><circle cx="7.5" cy="19.5" r="1.5"></circle><circle cx="17.5" cy="19.5" r="1.5"></circle></g></svg>`,
          name: 'Cart'
        },
        {
          svg: `<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" aria-hidden="true" role="img" width="1em" height="1em" preserveAspectRatio="xMidYMid meet" viewBox="0 0 24 24"><path d="M19.07 4.93a10 10 0 0 0-16.28 11a1.06 1.06 0 0 1 .09.64L2 20.8a1 1 0 0 0 .27.91A1 1 0 0 0 3 22h.2l4.28-.86a1.26 1.26 0 0 1 .64.09a10 10 0 0 0 11-16.28zM8 13a1 1 0 1 1 1-1a1 1 0 0 1-1 1zm4 0a1 1 0 1 1 1-1a1 1 0 0 1-1 1zm4 0a1 1 0 1 1 1-1a1 1 0 0 1-1 1z"></path></svg>`,
          name: 'Messages'
        },
        {
          svg: `<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" aria-hidden="true" role="img" width="22" height="22" preserveAspectRatio="xMidYMid meet" viewBox="0 0 24 24"><path d="M20.52 15.21l-1.8-1.81V8.94a6.86 6.86 0 0 0-5.82-6.88a6.74 6.74 0 0 0-7.62 6.67v4.67l-1.8 1.81A1.64 1.64 0 0 0 4.64 18H8v.34A3.84 3.84 0 0 0 12 22a3.84 3.84 0 0 0 4-3.66V18h3.36a1.64 1.64 0 0 0 1.16-2.79zM14 18.34A1.88 1.88 0 0 1 12 20a1.88 1.88 0 0 1-2-1.66V18h4z"></path></svg>`,
          name: 'Notifications'
        },
        {
          svg: `<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" aria-hidden="true" role="img" width="22" height="22" preserveAspectRatio="xMidYMid meet" viewBox="0 0 24 24"><path d="M22.56 16.3L14.89 3.58a3.43 3.43 0 0 0-5.78 0L1.44 16.3a3 3 0 0 0-.05 3A3.37 3.37 0 0 0 4.33 21h15.34a3.37 3.37 0 0 0 2.94-1.66a3 3 0 0 0-.05-3.04zM12 17a1 1 0 1 1 1-1a1 1 0 0 1-1 1zm1-4a1 1 0 0 1-2 0V9a1 1 0 0 1 2 0z"></path></svg>`,
          name: 'Logout'
        }
      ],
      active: 0,
      isOpen: false
    }
  },
  methods: {
    onClick(num) {
      this.active = num; 
    },
    setIsOpen() {
      this.isOpen = true;
    },
    setIsClose() {
      this.isOpen = false;
    }
  }
}
</script>
