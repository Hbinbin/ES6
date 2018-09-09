ES6 之前，不能直接为函数的参数指定默认值，只能采用变通的方法。

举个栗子：

    // 以前
    function info(name, age, wor) {
        var name = name || 'haobin',
            age = age || 18,
            work = work || 'web前端';
        // let [name, age, work] = [name || 'haobin', age || 18, work || 'web前端'];
        return '我是' + name + '，今年' + age + '，工作是' + work;
    }

    // 现在
    const info = ({name = 'haobin', age = 18, work = 'web前端'} = {}) => 
        return `我是${name}，今年${age}，工作是${work}`;
    }



