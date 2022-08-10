<template>
  <div id="publishingIndex">
    <h1>Daelim Museum Publishing Index</h1>
    <table>
      <colgroup>
        <col
          v-for="(item, index) in headers"
          :key="index"
          :style="`width: ${item.size}%;`"
        >
      </colgroup>
      <thead>
        <tr>
          <th
            v-for="(item, index) in headers"
            :key="index"
            :style="`width: ${item.px}px;`"
          >
            {{ item.name }}
          </th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="(item, index) in menuList"
          :key="index"
          :class="{
            ing:
              item.start !== '' &&
              item.start !== undefined &&
              item.start !== null,
            complete:
              item.end !== '' &&
              item.end !== undefined &&
              item.end !== null,
            modify:
              item.modify !== '' &&
              item.modify !== undefined &&
              item.modify !== null 
          }"
        >
          <td style="text-align: center;">
            {{ index + 1 }}
          </td>
          <td>{{ item.pageName }}</td>
          <td style="text-align: center;">
            {{ item.id }}
          </td>
          <td>
            <a
              :href="item.uri"
              target="_blank"
            >{{ item.uri }}</a>
          </td>
          <td>{{ item.start }}</td>
          <td>{{ item.end }}</td>
          <td>{{ item.modify }}</td>
          <td>{{ item.ver }}</td>
          <td v-html="item.notice" />
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import MenuList from '@/assets/publish/web-menu.js'

export default {
    name: 'PublishingIndex',
    data() {
        return {
            headers: [
                { name: 'No.', size: 3, px: 0 },
                { name: 'Page Name', size: 24, px: 0 },
                { name: 'ID', size: 7, px: 0 },
                { name: 'URI', size: 14, px: 0 },
                { name: 'Start', size: 7, px: 0 },
                { name: 'End', size: 7, px: 0 },
                { name: 'Modify', size: 7, px: 0 },
                { name: 'Ver.', size: 5, px: 0 },
                { name: 'Notice', size: 26, px: 0 }
            ],
            menuList: MenuList
        }
    },
    mounted() {
        this.headers.forEach((item, index) => {
            const mySize = screen.availWidth * (item.size / 100)
            item.px = mySize
        })
    }
}
</script>

<style lang="scss" scoped>
#publishingIndex {
  * { box-sizing: border-box; }
  h1 {
    width: 100%; height: 40px; line-height: 40px; padding: 0 20px; background: #eee; font-size: 18px; 
    position: fixed; top: 0; left: 0; z-index: 2;
  }
  table {
    table-layout: fixed; border-collapse: collapse; width: 100%; min-width: 1800px; position: relative; top: 70px;
    thead { 
      tr { width: 100%; position: fixed; top: 40px; left: 0; z-index: 2; }
    }
    th, td {
      border-bottom: 1px solid #ddd; padding: 8px 4px; position: relative;
    }
    th { background: #efd; height: 30px; }
    * { font-size: 12px; }
    th:after, td:after {
      width: 1px; height: 6px; content: ''; background: #ccc; position: absolute; top: 50%; left: 0; margin-top: -3px;
    }
    th:first-child:after, td:first-child:after {
      display: none;
    }
    tbody {
      tr {
        &.ing { 
          background: #ffd; 
          &.complete { 
            background: #dff; 
            &.modify { background: #add; }
          }
        }
      }
    }
  }
}
</style>
