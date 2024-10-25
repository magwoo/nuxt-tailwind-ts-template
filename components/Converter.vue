<script setup lang="ts">
    const valueFamilyNames = [" вес", " время", " скорость"];

    const convertValues = [
        { name: "кг.", family: 0, multiple: 1 },
        { name: "ц.", family: 0, multiple: 100 },
        { name: "т.", family: 0, multiple: 1000 },
        { name: "гр.", family: 0, multiple: 0.001 },
        { name: "мг.", family: 0, multiple: 0.000001 },
        { name: "нед.", family: 1, multiple: 24 * 7 },
        { name: "дн.", family: 1, multiple: 24 },
        { name: "ч.", family: 1, multiple: 1 },
        { name: "мин.", family: 1, multiple: 1 / 60 },
        { name: "сек.", family: 1, multiple: 1 / 60 / 60 },
        { name: "мсек.", family: 1, multiple: 1 / 60 / 60 / 1000 },
        { name: "км/ч", family: 2, multiple: 1 },
        { name: "км/с", family: 2, multiple: 3600 },
        { name: "м/ч", family: 2, multiple: 0.001 },
        { name: "м/мин", family: 2, multiple: 0.06 },
        { name: "м/с", family: 2, multiple: 3.6 },
        { name: "звук", family: 2, multiple: 1224 },
    ];

    let convertNames: string[] = [];
    valueFamilyNames.forEach((g, i) => {
        convertNames.push(g);
        convertNames.push(...convertValues.filter((v) => v.family == i).map((v) => v.name));
    });

    const resultConvertNames = ref<string[]>([])

    const input = ref<number>(0)
    const result = ref<number>(0)
    const selectedInputType = ref<string>(convertNames[1]);
    
    watch(selectedInputType, (selected: string) => {
        const valueName = convertValues.find((v) => v.name == selected);
        resultConvertNames.value = convertValues
            .filter((v) => v.family == valueName?.family)
            .map((v) => v.name);
    }, { immediate: true });

    const selectedResultType = ref<string>(resultConvertNames.value[0]);
    
    // watch([input, selectedInputType, selectedResultType], ([value]) => {
    //     const inputMult = convertValues.find((v) => v.name == selectedInputType.value)?.multiple!;
    //     const resultMult = convertValues.find((v) => v.name == selectedResultType.value)?.multiple!;
        
    //     const multiplier = inputMult / resultMult;
        
    //     result.value = value * multiplier;
    // });

    const calculate = () => {
        const inputMult = convertValues.find((v) => v.name == selectedInputType.value)?.multiple!;
        const resultMult = convertValues.find((v) => v.name == selectedResultType.value)?.multiple!;
        
        const multiplier = inputMult / resultMult * 1000;
        
        result.value = Math.round((input.value ?? 1) * multiplier) / 1000;
    };
</script>

<template>
    <section class='flex flex-col gap-12 items-center'>
        <h1 class='text-4xl text-stone-500 font-medium'>Конвертер</h1>
        <section class='flex gap-8 items-center'>
            <section class='flex gap-4'>
                <Input placeholder='Кол-во' type='number' v-model='input' />
                <Select :options='convertNames' @change='(v) => selectedInputType = v' />
            </section>
            <span class='text-stone-600 font-bold pb-1'>></span>
            <section class='flex gap-4'>
                <Input placeholder='Результат' type='number' v-model='result' />
                <Select :options='resultConvertNames' @change='(v) => selectedResultType = v' />
            </section>
        </section>
        <Button type='Primary' @click='calculate'>Перевести</Button>
    </section>
</template>
