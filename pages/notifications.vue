<script setup>
import { ref, computed } from "vue";

const messages = [
  {
    avatar: "https://xsgames.co/randomusers/avatar.php?g=female",
    isPrivate: false,
    author: "Mark Webber",
    message:
      "reacted to your recent post <strong>My first tournament today!</strong>",
    time: "1m ago",
    isRead: false,
  },
  {
    avatar: "https://xsgames.co/randomusers/avatar.php?g=female",
    isPrivate: false,
    author: "Angela Gray",
    message: "followed you",
    time: "5m ago",
    isRead: false,
  },
  {
    avatar: "https://xsgames.co/randomusers/avatar.php?g=female",
    isPrivate: false,
    author: "Jacob Thompson",
    message: "has joined your group <a href='/'>Chess Club</a>",
    time: "1 day ago",
    isRead: false,
  },
  {
    avatar: "https://xsgames.co/randomusers/avatar.php?g=female",
    isPrivate: true,
    author: "Rizky Hasanuddin",
    message:
      "Hello, thanks for setting up the Chess Club. I've been a member for a few weeks now and I'm already having lots of fun and improving my game",
    time: "5 days ago",
    isRead: true,
  },
  {
    avatar: "https://xsgames.co/randomusers/avatar.php?g=female",
    isPrivate: false,
    author: "Kimberly Smith",
    message: "commented on your picture",
    attach: "https://xsgames.co/randomusers/avatar.php?g=female",
    time: "1 week ago",
    isRead: true,
  },
  {
    avatar: "https://xsgames.co/randomusers/avatar.php?g=female",
    isPrivate: false,
    author: "Nathan Peterson",
    message:
      "reacted to your recent post <strong>5 end-game strategies to increase your win rate</strong>",
    tim: "2 weeks ago",
    isRead: true,
  },
  {
    avatar: "https://xsgames.co/randomusers/avatar.php?g=female",
    isPrivate: false,
    author: "Anna Kim",
    message: "left the group <a href='/'>Chess Club</a>",
    time: "2 weeks ago",
    isRead: true,
  },
];

const notifications = ref(messages);

const marAllAsRead = () => {
  notifications.value.forEach((notification) => (notification.isRead = true));
};

const notificationsCounter = computed(() => {
  return notifications.value.filter((e) => e.isRead === false).length;
});
</script>
<template>
  <main>
    <section class="notifications">
      <header class="notification-header">
        <h3 class="notification-title">
          Notifications
          <span class="notification-counter">{{ notificationsCounter }}</span>
        </h3>
        <button class="inline-button" @click="marAllAsRead">
          Mark all as read
        </button>
      </header>
      <div class="notifications-list">
        <article
          class="notifications-card"
          v-for="(
            { avatar, author, message, time, isRead, isPrivate, attach }, i
          ) in notifications"
          :key="i"
          :data-message-private="isPrivate"
          :data-is-read="isRead"
        >
          <img class="avatar" :src="avatar" alt="randomusers" />
          <div class="content">
            <template v-if="isPrivate">
              <strong class="author">{{ author }}</strong> sent you a private
              message
              <time class="time">{{ time }}</time>
              <span class="private" v-html="message"></span>
            </template>
            <template v-else>
              <strong class="author">{{ author }}</strong>
              <span v-html="message"></span>
              <span v-if="!isRead" class="isRead"></span>
              <time class="time">{{ time }}</time>
            </template>
          </div>
          <template v-if="attach">
            <img
              class="picture"
              src="https://xsgames.co/randomusers/avatar.php?g=female"
              alt="randomusers"
            />
          </template>
        </article>
      </div>
    </section>
  </main>
</template>
