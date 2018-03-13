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
        <td colspan="1" id="physic-ATK-effect">50</td>
        <td colspan="1" id="magic-ATK-effect">50</td>
        <td colspan="1" id="physic-DEF-effect">50</td>
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
    debuffLPhysicATK10: {
      name: "刀錆ノ呪詛(Ⅳ)",
      description: "单体、物攻",
      effectMin: {physicATK: 0.054, magicATK: 0, physicDEF: 0, magicDEF: 0},
      effectExpectation: {physicATK: 0.054, magicATK: 0, physicDEF: 0, magicDEF: 0},
      effectMax: {physicATK: 0.054, magicATK: 0, physicDEF: 0, magicDEF: 0}
    },
    debuffLPhysicATKDEF10: {
      name: "枷鎖ノ呪詛(Ⅲ)",
      description: "单体、物攻物防",
      effectMin: {physicATK: 0.049, magicATK: 0, physicDEF: 0.088, magicDEF: 0},
      effectExpectation: {physicATK: 0.049, magicATK: 0, physicDEF: 0.088, magicDEF: 0},
      effectMax: {physicATK: 0.049, magicATK: 0, physicDEF: 0.088, magicDEF: 0}
    },
    debuffLAllATK15: {
      name: "腐蝕ノ呪術(Ⅲ)",
      description: "1~2体、物攻魔攻",
      effectMin: {physicATK: 0.044, magicATK: 0.044, physicDEF: 0, magicDEF: 0},
      effectExpectation: {physicATK: 0.066, magicATK: 0.066, physicDEF: 0, magicDEF: 0},
      effectMax: {physicATK: 0.088, magicATK: 0.088, physicDEF: 0, magicDEF: 0}
    },
    debuffLAllATK10: {
      name: "腐蝕ノ呪詛(Ⅲ)",
      description: "1体、物攻魔攻",
      effectMin: {physicATK: 0.051, magicATK: 0.051, physicDEF: 0, magicDEF: 0},
      effectExpectation: {physicATK: 0.051, magicATK: 0.051, physicDEF: 0, magicDEF: 0},
      effectMax: {physicATK: 0.051, magicATK: 0.051, physicDEF: 0, magicDEF: 0}
    },
    debuffLAllDEF10: {
      name: "落城ノ呪詛(Ⅲ)",
      description: "单体、物防魔防",
      effectMin: {physicATK: 0, magicATK: 0, physicDEF: 0.088, magicDEF: 0.088},
      effectExpectation: {physicATK: 0, magicATK: 0, physicDEF: 0.088, magicDEF: 0.088},
      effectMax: {physicATK: 0, magicATK: 0, physicDEF: 0.088, magicDEF: 0.088}
    },
    debuffLAllDEF15: {
      name: "落城ノ呪術(Ⅲ)",
      description: "1~2体、物防魔防",
      effectMin: {physicATK: 0, magicATK: 0, physicDEF: 0.072, magicDEF: 0.072},
      effectExpectation: {physicATK: 0, magicATK: 0, physicDEF: 0.108, magicDEF: 0.108},
      effectMax: {physicATK: 0, magicATK: 0, physicDEF: 0.144, magicDEF: 0.144}
    },
    debuffLPhysicDEF20: {
      name: "壊壁ノ呪術(Ⅱ)",
      description: "2体、物防",
      effectMin: {physicATK: 0, magicATK: 0, physicDEF: 0.124, magicDEF: 0},
      effectExpectation: {physicATK: 0, magicATK: 0, physicDEF: 0.124, magicDEF: 0},
      effectMax: {physicATK: 0, magicATK: 0, physicDEF: 0.124, magicDEF: 0}
    },
    debuffLPhysicDEF15: {
      name: "壊壁ノ呪術(Ⅲ)",
      description: "1~2体、物防",
      effectMin: {physicATK: 0, magicATK: 0, physicDEF: 0.079, magicDEF: 0},
      effectExpectation: {physicATK: 0, magicATK: 0, physicDEF: 0.1135, magicDEF: 0},
      effectMax: {physicATK: 0, magicATK: 0, physicDEF: 0.158, magicDEF: 0}
    },
    debuffLPhysicDEF10: {
      name: "壊壁ノ呪詛(Ⅳ)",
      description: "单体、物防",
      effectMin: {physicATK: 0, magicATK: 0, physicDEF: 0.095, magicDEF: 0},
      effectExpectation: {physicATK: 0, magicATK: 0, physicDEF: 0.095, magicDEF: 0},
      effectMax: {physicATK: 0, magicATK: 0, physicDEF: 0.095, magicDEF: 0}
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
