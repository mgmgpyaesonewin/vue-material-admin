<template>
  <v-container grid-list-xl fluid>
    <v-layout row wrap>
      <v-flex sm12>
        <h3>Drivers' status</h3>
      </v-flex>
      <v-flex lg12>
        <v-card>
          <v-toolbar card color="white">
            <v-flex xs4>
              <v-text-field
                flat
                solo
                prepend-icon="search"
                placeholder="Type something"
                v-model="search"
                hide-details
                class="hidden-sm-and-down"
              ></v-text-field>
            </v-flex>
            <v-flex xs8>
              <v-select
                v-model="value"
                :items="items"
                attach
                small-chips
                deletable-chips
                prepend-inner-icon="calendar_view_day"
                multiple
              ></v-select>
            </v-flex>
          </v-toolbar>
          <v-divider></v-divider>
          <v-card-text class="pa-0">
            <v-data-table
              :headers="complex.headers"
              :search="search"
              :items="drivers"
              :rows-per-page-items="[10, 25, 50, { text: 'All', value: -1 }]"
              class="elevation-1"
              item-key="name"
              select-all
              v-model="complex.selected"
            >
              <template slot="items" slot-scope="props">
                <td>
                  <v-checkbox
                    primary
                    hide-details
                    v-model="props.selected"
                  ></v-checkbox>
                </td>
                <td>
                  <v-avatar size="32">
                    <img :src="props.item.avatar" alt="" />
                  </v-avatar>
                </td>
                <td>{{ props.item.name }}</td>
                <td>{{ props.item.email }}</td>
                <td>{{ props.item.phone }}</td>
                <td class="text-xs-left">
                  <v-chip
                    label
                    small
                    :color="getColorByStatus(props.item.status)"
                    text-color="white"
                  >
                    {{ props.item.status }}
                  </v-chip>
                </td>
                <td>
                  <v-btn depressed outline icon fab dark color="primary" small>
                    <v-icon>edit</v-icon>
                  </v-btn>
                  <v-btn depressed outline icon fab dark color="pink" small>
                    <v-icon>delete</v-icon>
                  </v-btn>
                </td>
              </template>
            </v-data-table>
          </v-card-text>
        </v-card>
      </v-flex>
    </v-layout>
    <register-form />
  </v-container>
</template>

<script>
import { Items as Users } from "@/api/user";
import RegisterFrom from "@/components/drivers/RegisterForm.vue";
export default {
  components: {
    "register-form": RegisterFrom
  },
  data() {
    return {
      dialog: false,
      search: "",
      items: [
        "freelance",
        "munch",
        "assigned",
        "unassigned",
        "external",
        "offduty"
      ],
      value: [],
      complex: {
        selected: [],
        headers: [
          {
            text: "Avatar",
            value: "avatar"
          },
          {
            text: "Name",
            value: "name"
          },
          {
            text: "Email",
            value: "email"
          },
          {
            text: "Phone",
            value: "phone"
          },
          {
            text: "Status",
            value: "status"
          },
          {
            text: "Action",
            value: ""
          }
        ],
        items: Users
      },
      colors: {
        munch: "blue",
        freelance: "accent",
        external: "green",
        assigned: "blue",
        unassigned: "yellow",
        offduty: "red"
      }
    };
  },
  methods: {
    getColorByStatus(status) {
      return this.colors[status];
    }
  },
  computed: {
    drivers() {
      if (this.value.length === 0) {
        return Users;
      }
      return Users.filter(function(user) {
        return this.indexOf(user.status) >= 0;
      }, this.value);
    }
  }
};
</script>
