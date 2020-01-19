<template>
<div>
  <v-card
    max-width="1000"
    class="mx-auto"
  >
    <v-list-item>
      <v-list-item-avatar><img :src="avatar"></v-list-item-avatar>
      <v-list-item-content style="text-align: left;">
        <v-list-item-title><strong>{{title}}</strong></v-list-item-title>
        <v-list-item-subtitle>Автор: {{author}}</v-list-item-subtitle>
      </v-list-item-content>
    </v-list-item>

    <v-card-text style="text-align: left;">
      {{body}}
    </v-card-text>

    <v-card-actions>
      <v-spacer></v-spacer>
      <v-btn icon>
        <v-icon>mdi-heart</v-icon>
      </v-btn>
      <v-btn icon>
        <v-icon>mdi-bookmark</v-icon>
      </v-btn>
      <v-btn icon>
        <v-icon>mdi-share-variant</v-icon>
      </v-btn>
    </v-card-actions>
  </v-card>
  <br><br>
</div>
</template>

<script>
export default {
  props: ['title', 'body', 'author', 'avatar'],
  data: () => ({
  }),
}
</script>
