ES6 之前，不能直接为函数的参数指定默认值，只能采用变通的方法。

    const info = (name, age, work) => {
        //let name = name || 'haobin',
        //    age = age || 18,
        //    work = work || 'web前端';
        let [name, age, work] = [name || 'haobin', age || 18, work || 'web前端'];
        return `${name}今年${age}工作是${work}`;
    }



