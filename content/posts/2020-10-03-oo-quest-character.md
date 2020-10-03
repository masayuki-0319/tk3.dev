---
title: キャラクターの能力を考える
date: 2020-10-03T23:41:52+09:00
slug: 74dac2d183366bcbb8a4906c4010f12a67ef71b6
---
戦闘がメインで、ダンジョンを探索する冒険者。種族あり、職業あり、魔法あり。そんな世界にしたいと考えている。それを踏まえ、キャラクターの基礎能力を考えた。本当に基礎だけ。能力値を考えるとき、Wizardry を思い浮かべたが、参考程度に。

物理攻撃で戦闘ができるくらいまでを考える。レベルや職業、ボスなどを考えたときに、バランス調整がしやすいとか、考えることは沢山ある。

- 力（STRENGTH）
  - 攻撃力に影響。職業ボーナスを付けるかも。
- 知力（INTELLIGENCE）
  - 魔法攻撃力に影響。魔法抵抗の条件に使うかも。
  - 魔法を覚える条件に使うかも。
  - 呪文の覚えやすさ、呪文のダメージや成功率にも影響
- 生命力（VITALITY）
  - ヒットポイント（HP）に影響。レベルアップ時のHP上昇量に影響。
  - 魔法抵抗の際に判定に使うかも。
  - 蘇生呪文の判定で使うかも。
- 器用さ（DEXTERITY）
  - 命中に影響。
  - 回避に影響するかも。
  - 罠や扉の解除判定に使うかも。
- すばやさ（AGILITY）
  - 回避に影響。
  - 命中に影響するかも。
- 運の強さ（LUCK）
  - 何か不運なできごとが起きたときに。

ざっとこんな感じだろう。動かしながら調整はしていく。能力値の下限値と上限値は未定。これらが影響する攻撃力や命中力、回避は次の機会に。


コードにしてみると、こんな感じだろうか。形だけ。ちなみにコードは Scala で記述している。

```
class Character(
  name: String,
  strength: Int,
  intelligence: Int,
  vitality: Int,
  dexterity: Int,
  agility: Int,
  luck: Int
) {
  def doSomething():Unit = {
    println(s"$name tries to do something.")
  }
}

object Main {
  def main(args: Array[String]): Unit = {
    val character1 = new Character("character1", 10, 10, 10, 10, 10, 10)
    val character2 = new Character("character2", 10, 10, 10, 10, 10, 10)

    println("start game...")

    character1.doSomething()
    character2.doSomething()
  }
}
```

