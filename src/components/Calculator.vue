<template>
  <div>
    <h1>{{ debuffEffectTitle }}</h1>
    <table border="1" class="result-table" id="debuff-effect">
      <tr>
        <td colspan="2">攻debuff</td>
        <td colspan="2">防debuff</td>
      </tr>
      <tr>
        <td colspan="2">100</td>
        <td colspan="2">100</td>
      </tr>
      <tr>
        <td colspan="1">物攻debuff</td>
        <td colspan="1">魔攻debuff</td>
        <td colspan="1">物防debuff</td>
        <td colspan="1">魔防debuff</td>
      </tr>
      <tr>
        <td colspan="1" id="physical-ATK-effect">50</td>
        <td colspan="1" id="magic-ATK-effect">50</td>
        <td colspan="1" id="physical-DEF-effect">50</td>
        <td colspan="1" id="magic-DEF-effect">50</td>
      </tr>
    </table>
  </div>
</template>

<script>
  const activeSkillDatabase = {
    debuffLMagicATK10: {
      name: "衰弱ノ呪詛(Ⅳ)",
      description: "单体、魔攻",
      effectMin: {physicATK: 0, magicATK: 0.054, physicDEF: 0, magicDEF: 0},
      effectExpectation: {physicATK: 0, magicATK: 0.054, physicDEF: 0, magicDEF: 0},
      effectMax: {physicATK: 0, magicATK: 0.054, physicDEF: 0, magicDEF: 0}
    },
    debuffLMagicATK15: {
      name: "衰弱ノ呪術(Ⅲ)",
      description: "1~2体、魔攻",
      effectMin: {physicATK: 0, magicATK: 0.044, physicDEF: 0, magicDEF: 0},
      effectExpectation: {physicATK: 0, magicATK: 0.066, physicDEF: 0, magicDEF: 0},
      effectMax: {physicATK: 0, magicATK: 0.088, physicDEF: 0, magicDEF: 0}
    },
    debuffLMagicATKDEF15: {
      name: "破魔ノ呪術(Ⅲ)",
      description: "1~2体、魔防魔攻",
      effectMin: {physicATK: 0, magicATK: 0.044, physicDEF: 0, magicDEF: 0.072},
      effectExpectation: {physicATK: 0, magicATK: 0.066, physicDEF: 0, magicDEF: 0.108},
      effectMax: {physicATK: 0, magicATK: 0.088, physicDEF: 0, magicDEF: 0.144}
    },
    debuffLPhysicalATK10: {
      name: "刀錆ノ呪詛(Ⅳ)",
      description: "单体、物攻",
      effectMin: {physicATK: 0.54, magicATK: 0, physicDEF: 0, magicDEF: 0},
      effectExpectation: {physicATK: 0.54, magicATK: 0, physicDEF: 0, magicDEF: 0},
      effectMax: {physicATK: 0.54, magicATK: 0, physicDEF: 0, magicDEF: 0}
    },
    debuffLPhysicalATK10: {
      name: "刀錆ノ呪詛(Ⅳ)",
      description: "单体、物攻",
      effectMin: {physicATK: 0.54, magicATK: 0, physicDEF: 0, magicDEF: 0},
      effectExpectation: {physicATK: 0.54, magicATK: 0, physicDEF: 0, magicDEF: 0},
      effectMax: {physicATK: 0.54, magicATK: 0, physicDEF: 0, magicDEF: 0}
    },
  };

  export default {
    name: 'Calculator',
    data() {
      return {
        debuffEffectTitle: 'debuff总览'
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  table {
    align: center;
  }

</style>
