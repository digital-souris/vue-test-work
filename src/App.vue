<template>
  <div id="app">
    <div class="block">
      <div class="block__content">
        <template v-if="getBlock.type === 'start'">
          <button @click="goToBlock(getBlock.push)">Start</button>
        </template>
        <template v-else-if="getBlock.type === 'finish'">
          <button @click="clearBlocks">Выйти из чата</button>

        </template>
        <template v-else>
          <span v-if="getBlock.type === 'text'">Это: {{getBlock.block}} блок</span>
          <span v-else>Ответ</span>
          <br/>
          <template v-if="Array.isArray(getBlock.push)">
            <button v-for="(item, index) in getBlock.push" @click="goToBlock(item)" :key="index">
              Go to {{item}}
            </button>
          </template>
          <template v-else>
            <button @click="goToBlock(getBlock.push)">
              Go to {{getBlock.push}}
            </button>
          </template>
        </template>
      </div>
    </div>
    <div class="percent">
      {{percent}} %
    </div>
  </div>
</template>

<script>
import {find, maxBy} from "lodash";

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
      activeBlock: 0,
      percent: 0
    }
  },
  computed: {
    getBlock() {
      return find(this.blocks, block => block.block === this.activeBlock) || {}
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
