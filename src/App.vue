<template>
  <div id="app">
    {{ getBlocksToTest }}
    <div class="block">
      <div class="block__content">
        <template v-if="getBlock.type === 'start'">
          <button @click="goToBlock(getBlock.push)">Start</button>
        </template>
        <template v-else-if="getBlock.type === 'finish'">
          <button @click="clearBlocks">Выйти из чата</button>

        </template>
        <template v-else>
          <span v-if="getBlock.type === 'text'">Это: {{ getBlock.block }} блок</span>
          <span v-else>Ответ</span>
          <br/>
          <template v-if="Array.isArray(getBlock.push)">
            <button v-for="(item, index) in getBlock.push" @click="goToBlock(item)" :key="index">
              Go to {{ item }}
            </button>
          </template>
          <template v-else>
            <button @click="goToBlock(getBlock.push)">
              Go to {{ getBlock.push }}
            </button>
          </template>
        </template>
      </div>
    </div>
    <div class="percent">
      {{ percent }} %
    </div>
  </div>
</template>

<script>
import {find, findIndex, forEach, maxBy} from "lodash";

export default {
  name: 'App',
  data() {
    return {
      blocks: [
        {
          type: 'start',
          push: 1,
          level: 0,
          block: 0,
        },
        {
          type: 'text',
          text: 'Hetty',
          push: 2,
          alias: 'D3C682',
          level: 1,
          block: 1,
        },
        {
          type: 'ask',
          push: [3, 4],
          alias: 'D3C683',
          level: 2,
          block: 2,

        },
        {
          alias: 'D3C684',
          type: 'text',
          push: 5,
          level: 3,
          block: 3,

        },
        {
          alias: 'D3C685',
          type: "text",
          push: 1,
          level: 3,
          block: 4,
        },
        {
          alias: 'D3C686',
          type: 'text',
          push: 6,
          level: 4,
          block: 5
        },
        {
          alias: 'D3C687',
          type: 'text',
          push: 7,
          level: 5,
          block: 6
        },
        {
          alias: 'D3C688',
          level: 6,
          type: 'ask',
          push: [8, 9, 10],
          block: 7,
        },
        {
          alias: 'D3C689',
          level: 7,
          type: 'text',
          push: 11,
          block: 8
        },
        {
          level: 7,
          alias: 'D3C690',
          type: 'text',
          push: 13,
          block: 9
        },
        {
          level: 7,
          alias: 'D3C691',
          type: 'text',
          push: 15,
          block: 10
        },
        {
          alias: 'D3C695',
          level: 8,
          type: 'text',
          block: 11,
          push: 12
        },
        {
          alias: 'D3C696',
          block: 12,
          level: 9,
          type: 'text',
          push: 14
        },
        {
          block: 13,
          alias: 'D3C697',
          level: 9,
          push: 15,
          type: 'text'
        },
        {
          block: 14,
          alias: 'D3C698',
          level: 10,
          push: 16,
          type: 'text'
        },
        {
          alias: 'D3C694',
          level: 9,
          block: 15,
          type: 'ask',
          push: [16, 6]
        },
        {
          level: 11,
          alias: 'D3C699',
          block: 16,
          type: 'finish'
        }
      ],
      dataToTest: {
        "last_node_id": 3,
        "last_link_id": 2,
        "nodes": [{
          "id": 2,
          "type": "SYSTEM/end",
          "pos": [500, 100],
          "size": {"0": 140, "1": 26},
          "flags": {},
          "order": 2,
          "mode": 0,
          "inputs": [{"name": "", "type": "number", "link": 2}],
          "properties": {"ACTION_ID": "END"},
          "shape": 1
        }, {
          "id": 1,
          "type": "SYSTEM/start",
          "pos": [10, 100],
          "size": {"0": 140, "1": 26},
          "flags": {},
          "order": 0,
          "mode": 0,
          "outputs": [{"name": "", "type": "number", "links": [1]}],
          "properties": {"ACTION_ID": "START"},
          "shape": 1
        }, {
          "id": 3,
          "type": "GAME/enterChat",
          "pos": [279, 237],
          "size": {"0": 210, "1": 58},
          "flags": {},
          "order": 1,
          "mode": 0,
          "inputs": [{"name": "", "type": "number", "link": 1}],
          "outputs": [{"name": "", "type": "number", "links": [2]}],
          "properties": {"chat": 19, "ACTION_ID": "182273", "ACTION_IN": "3D10D3"},
          "widgets_values": ["Jessica"],
          "subgraph": {
            "last_node_id": 9,
            "last_link_id": 9,
            "nodes": [{
              "id": 1,
              "type": "SYSTEM/EnterChatInput",
              "pos": [-537, -23],
              "size": {"0": 210, "1": 62},
              "flags": {},
              "order": 0,
              "mode": 0,
              "outputs": [{"name": "", "type": "number", "links": [1]}],
              "properties": {
                "who": 21,
                "message": "Hello World! Block 0",
                "ACTION_ID": "3D10D3",
                "PARENT_ID": "",
                "chat": 19
              },
              "shape": 1
            }, {
              "id": 3,
              "type": "GAME/message",
              "pos": [-494, 140],
              "size": {"0": 210, "1": 86},
              "flags": {"clip_area": true},
              "order": 1,
              "mode": 0,
              "inputs": [{"name": "", "type": "number", "link": 1}, {
                "name": "",
                "type": "number",
                "link": 5
              }, {"name": "", "type": "number", "link": null}],
              "outputs": [{"name": "", "type": "number", "links": [2]}],
              "properties": {"who": 21, "message": "Block 1", "ACTION_ID": "F44DF2", "save": true},
              "widgets_values": ["Hetty", "Block 1", true]
            }, {
              "id": 4,
              "type": "GAME/answer",
              "pos": [-200.55205021096066, 143.89721201528045],
              "size": {"0": 210, "1": 110},
              "flags": {},
              "order": 2,
              "mode": 0,
              "inputs": [{"name": "", "type": "number", "link": 2}, {
                "name": "",
                "type": "number",
                "link": null
              }, {"name": "", "type": "number", "link": null}],
              "outputs": [{"name": "1", "type": "number", "links": [3]}, {
                "name": "2",
                "type": "number",
                "links": [4]
              }, {"name": "3", "type": "number", "links": null}],
              "properties": {
                "text_1": "To Block 3",
                "text_2": "To Block 4",
                "text_3": "",
                "ACTION_ID": "66C2C1",
                "improve": false
              },
              "widgets_values": ["To Block 3", "To Block 4", "", false]
            }, {
              "id": 6,
              "type": "GAME/message",
              "pos": [-231, 452],
              "size": {"0": 210, "1": 86},
              "flags": {"clip_area": true},
              "order": 4,
              "mode": 0,
              "inputs": [{"name": "", "type": "number", "link": 4}, {
                "name": "",
                "type": "number",
                "link": null
              }, {"name": "", "type": "number", "link": null}],
              "outputs": [{"name": "", "type": "number", "links": [5]}],
              "properties": {"who": 21, "message": "Next Block 1", "ACTION_ID": "0EB41F", "save": false},
              "widgets_values": ["Hetty", "Next Block 1", false]
            }, {
              "id": 5,
              "type": "GAME/message",
              "pos": [97, -12],
              "size": {"0": 210, "1": 86},
              "flags": {"clip_area": true},
              "order": 3,
              "mode": 0,
              "inputs": [{"name": "", "type": "number", "link": 3}, {
                "name": "",
                "type": "number",
                "link": null
              }, {"name": "", "type": "number", "link": null}],
              "outputs": [{"name": "", "type": "number", "links": [6]}],
              "properties": {
                "who": 21,
                "message": "This is block 3 Next Block 5",
                "ACTION_ID": "6140BC",
                "save": false
              },
              "widgets_values": ["Hetty", "This is block 3 Next Block 5", false]
            }, {
              "id": 7,
              "type": "GAME/message",
              "pos": [441, 165],
              "size": {"0": 210, "1": 86},
              "flags": {"clip_area": true},
              "order": 5,
              "mode": 0,
              "inputs": [{"name": "", "type": "number", "link": 6}, {
                "name": "",
                "type": "number",
                "link": null
              }, {"name": "", "type": "number", "link": null}],
              "outputs": [{"name": "", "type": "number", "links": [7]}],
              "properties": {"who": 21, "message": "This is block 5", "ACTION_ID": "87A5D2", "save": false},
              "widgets_values": ["Hetty", "This is block 5", false]
            }, {
              "id": 8,
              "type": "GAME/message",
              "pos": [738, 180],
              "size": {"0": 210, "1": 86},
              "flags": {"clip_area": true},
              "order": 6,
              "mode": 0,
              "inputs": [{"name": "", "type": "number", "link": 7}, {
                "name": "",
                "type": "number",
                "link": null
              }, {"name": "", "type": "number", "link": null}],
              "outputs": [{"name": "", "type": "number", "links": [8]}],
              "properties": {"who": 21, "message": "This is block 6", "ACTION_ID": "CBC348", "save": false},
              "widgets_values": ["Hetty", "This is block 6", false]
            }, {
              "id": 9,
              "type": "GAME/message",
              "pos": [1104, 105],
              "size": {"0": 210, "1": 86},
              "flags": {"clip_area": true},
              "order": 7,
              "mode": 0,
              "inputs": [{"name": "", "type": "number", "link": 8}, {
                "name": "",
                "type": "number",
                "link": null
              }, {"name": "", "type": "number", "link": null}],
              "outputs": [{"name": "", "type": "number", "links": [9]}],
              "properties": {"who": 21, "message": "This is block 7. To End", "ACTION_ID": "EE5E26", "save": false},
              "widgets_values": ["Hetty", "This is block 7. To End ", false]
            }, {
              "id": 2,
              "type": "SYSTEM/EnterChatOutput",
              "pos": [1283, -51],
              "size": {"0": 140, "1": 66},
              "flags": {},
              "order": 8,
              "mode": 0,
              "inputs": [{"name": "", "type": "number", "link": 9}, {
                "name": "",
                "type": "number",
                "link": null
              }, {"name": "", "type": "number", "link": null}],
              "properties": {"ACTION_ID": "3FD9B9", "PARENT_ID": ""},
              "shape": 1
            }],
            "links": [[1, 1, 0, 3, 0, "number"], [2, 3, 0, 4, 0, "number"], [3, 4, 0, 5, 0, "number"], [4, 4, 1, 6, 0, "number"], [5, 6, 0, 3, 1, "number"], [6, 5, 0, 7, 0, "number"], [7, 7, 0, 8, 0, "number"], [8, 8, 0, 9, 0, "number"], [9, 9, 0, 2, 0, "number"]],
            "groups": [],
            "config": {},
            "extra": {},
            "version": 0.4
          }
        }],
        "links": [[1, 1, 0, 3, 0, "number"], [2, 3, 0, 2, 0, "number"]],
        "groups": [],
        "config": {},
        "extra": {},
        "version": 0.4
      },
      activeBlock: 0,
      percent: 0
    }
  },
  computed: {
    getBlock() {
      return find(this.blocks, block => block.block === this.activeBlock) || {}
    },
    getBlocksToTest() {
      const blockItems = this.dataToTest.nodes[2].subgraph.nodes
      forEach(blockItems, (block) => {
        if (block.outputs && block.outputs.length) {
          forEach(block.outputs, output => {
            if (output.links) {
              const index = findIndex(blockItems, item => item.order === output.links[0])
              console.log(index)
              if (index !== -1) {
                blockItems[index].properties.level = (block.properties.level || 0) + 1
              }
            }

          })
        }
        if (!block.properties.level) {
          block.properties.level = 0
        }
      })
      return blockItems
    },
    getPercentPath() {
      const maxLevel = maxBy(this.blocks, 'level')?.level || 1
      return Math.round((this.getBlock.level / maxLevel * 100))
    }
  },
  watch: {
    getPercentPath(val) {
      this.percent = this.percent < val ? val : this.percent
    }
  },
  methods: {
    goToBlock(block) {
      this.activeBlock = block
    },
    clearBlocks() {
      this.percent = 0
      this.activeBlock = 0
    }
  }
}
</script>
<style lang="scss" scoped>
.block {
  width: 300px;
  padding: 15px;
  border-radius: 5px;
  border: 1px solid #000;
  cursor: pointer;
  text-align: center;

  button {
    display: block;
    width: 90%;
    margin: 0 auto;
  }
}

.percent {
  text-align: center;
  width: 300px;
  padding-top: 25px;
}
</style>
