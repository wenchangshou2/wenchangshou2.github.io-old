---
title: ts 实现混合类
date: 2019-10-18 15:05:47
tags: typescript
---

ts混合类特性
<!--more-->

``` javascript
class Mammal{
    breathe():string{
        return "I'm alive!"
    }
}
class WingedAnimal {
    fly() :string{
        return "I can fly!"
    }
}
class Bat implements Mammal,WingedAnimal{
    breathe:()=>string;
    fly: () => string;
}
function applyMixins(derivedCtor:any,baseCtors:any[]){
    baseCtors.forEach(baseCtor=>{
        Object.getOwnPropertyNames(baseCtor.prototype).forEach(name=>{
            if(name!=='constructor'){
                derivedCtor.prototype[name]=baseCtor.prototype[name];
            }
        })
    })
}
applyMixins(Bat,[Mammal,WingedAnimal])
var bat=new Bat();
console.log(bat.breathe());
console.log(bat.fly());
```