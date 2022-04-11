<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <v-img
          :src="require('../assets/logo.png')"
          class="my-3"
          contain
          height="200"
        />
      </v-col>

      <v-card class="mx-auto">
        <v-navigation-drawer width="100%">
          <v-list-item>
            <v-list-item-content>
              <v-list-item-title class="text-h6">
                Ship Mod Manager
              </v-list-item-title>
            </v-list-item-content>
          </v-list-item>

          <v-divider></v-divider>

          <v-data-table
            dense
            :search="search"
            :headers="headers"
            :items="ships"
            hide-default-footer
          >
            <template v-slot:item.base="{ item }">
              <v-tooltip bottom>
                <template v-slot:activator="{ on, attrs }">
                  <v-icon v-bind="attrs" v-on="on">
                    {{
                      item.base
                        ? "mdi-home-circle-outline"
                        : "mdi-progress-wrench"
                    }}
                  </v-icon>
                </template>
                <span>
                  {{ item.base ? "Included in base game" : "Modded ship" }}
                </span>
              </v-tooltip>
            </template>
            <template v-slot:item.include="{ item }">
              <v-checkbox
                :input-value="item.include"
                v-model="item.include"
              ></v-checkbox>
            </template>
            <template v-slot:item.weight="{ item }">
              <v-text-field
                dense
                :value="item.weight"
                v-model="item.weight"
                :rules="weightRules"
                hide-details="auto"
              ></v-text-field>
            </template>
          </v-data-table>
          <v-container>
            <v-btn>Save changes</v-btn>
          </v-container>
        </v-navigation-drawer>
      </v-card>
    </v-row>
  </v-container>
</template>

<script lang="ts">
import { defineComponent, onMounted, ref } from "@vue/composition-api";

export default defineComponent({
  setup() {
    const weightRules = [
      (value) => {
        return RegExp("^[0-9]*$").test(value) ? true : "Value must be a number";
      },
    ];
    const search = ref("");

    const headers = ref([
      {
        text: "Base / Mod",
        value: "base",
      },
      {
        text: "Include?",
        value: "include",
      },
      {
        text: "Ship Name",
        value: "name",
      },
      {
        text: "Weight",
        value: "weight",
      },
    ]);

    const ships = ref([]);

    onMounted(async () => {
      ships.value.push(
        {
          base: true,
          include: true,
          name: "test test test test test test ship",
          weight: 3,
        },
        {
          base: false,
          include: false,
          name: "test ship",
          weight: 5,
        }
      );
    });

    return {
      weightRules,
      search,
      ships,
      headers
    };
  },
});
</script>

