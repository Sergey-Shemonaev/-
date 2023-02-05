<script>

    $: visible =true;
    $: visibleRedaction = false;
    function visibleBocks() {
        visible = !visible
    };

    $: arrVisiriors=[
            {
            фио:'Валентин АВТУХОВ',
            телефон: +7985654654
        },
        {
            фио:'Даяна ОВСЯНКИН',
            телефон: +7654987341321
        },
        {
            фио:'Захар ФАБРИЧНЫЙ',
            телефон: +75498734321
        },
        {
            фио:'Мелания МАГНИЦКИЙ' ,
            телефон: +76987321},
        {
            фио:' Нонна ВАГИН',
            телефон: +7658734321},
        {
            фио:' Ямато ГАВРИШОВ',
            телефон: +765731321
        }
    ];
    $: sortStron = true;
    const sortArrs = (fieldName, повозраст) => {
        if(повозраст){
            arrVisiriors.sort((a, b)=>{
                if(a[fieldName] < b[fieldName]) return 1;
                else if (a[fieldName] > b[fieldName]) return -1;
                else  return 0;
            })

        }
        if(!повозраст){
            arrVisiriors.sort((a, b)=>{
                if(a[fieldName] < b[fieldName]) return -1;
                else if (a[fieldName] > b[fieldName]) return 1;
                else  return 0;
            })

        }
        arrVisiriors= [...arrVisiriors]
    }
    const sortOptions = [
        {
            title:'Ф И О',
            value: 'фио'
        }, {

            title: 'по телефон',
            value: 'телефон'
        }
    ]



    $: marker = 0;
    let inputФиоRedackt = '';
    let inputтелефонRedackt = '';

    let inputФио = '';
    let inputтелефон = '';
    let selected = sortOptions[0]
    const saveBocks = ()=> {
        const newBocks = {
            фио: inputФио,
            телефон: inputтелефон,

        }
        arrVisiriors = [...arrVisiriors, newBocks]
        visible = !visible
    };

    const editBocks =(id)=>{
        marker = id;
        console.log(id)
        inputФиоRedackt = arrVisiriors[marker].фио
        inputтелефонRedackt = arrVisiriors[marker].телефон

        visibleRedaction = !visibleRedaction;
    }

    const saveEditBocks = (id) =>{
        arrVisiriors[id] ={
            фио: inputФиоRedackt,
            телефон: inputтелефонRedackt,

        }
        console.log(id)
        arrVisiriors = [...arrVisiriors]
        visibleRedaction = !visibleRedaction
    }

    /           Поиск                                                      /

    let visilbeSaerch = false;
    let visibleDock = true;
    $: coppy = [];
    $: inputSearch = '';
    let searchButton = true;
    let inputField;
    $: currentQues = []

    const searchFunk = () => {
        coppy = arrVisiriors;
        currentQues = arrVisiriors.filter((el)=>el.фио.toLocaleLowerCase().includes(inputSearch.toLocaleLowerCase()) && el !== inputSearch);
        console.log(currentQues)
        arrVisiriors = currentQues;
        searchButton = !searchButton;
        visilbeSaerch =!visilbeSaerch;
        visibleDock =!visibleDock;
    };
    const searchReset = () => {
        arrVisiriors = coppy;
        searchButton = !searchButton
        inputField.value = '';
        visilbeSaerch =!visilbeSaerch;
        visibleDock =!visibleDock;
    };

</script>
<div class="contenier">
    <div id="visitior">
        <section>
            <div class="allCards">
                <div>
                    <h4>ALL VISITORS</h4>
                </div>
                <div>
                    <button on:click={visibleBocks}>New visitior</button>
                </div>
            </div>
            <div class="space_betvin">
                <div>
                    <span>   ортировка по:</span>
                    <select bind:value={selected.value}>
                        {#each sortOptions as option}
                            <option value={option.value}>{option.title}</option>
                        {/each}
                    </select>
                    <button on:click={()=>{
                        sortStron = !sortStron;
                        sortArrs(selected.value, sortStron)
                    }}>Sort</button>
                </div>
                <div>
                    <span>Поиск</span>
                    <input bind:this={inputField} type="searchText" name="" id=""
                           on:input={(e)=>{
                            inputSearch = e.target.value
                            console.log(inputSearch)
                            }}>
                    {#if searchButton}
                        <button on:click={searchFunk}>Поиск</button>
                    {:else}
                        <button on:click={searchReset} style="color: red">Сброс</button>
                    {/if}
                </div>
            </div>
        </section>
        <section>
            <table>
                <thead>
                <tr>
                    <th style="width: 20%">ID</th>
                    <th style="width: 40%">ФИО</th>
                    <th style="width: 40%">Телефон</th>
                    <th style="width: 20%">Редактирование</th>
                </tr>
                </thead>
                <tbody>
                {#if  visibleDock}
                    {#each arrVisiriors as strings, index}
                        <tr>
                            <td> {index +=1}</td>
                            <td> {strings.фио}</td>
                            <td> {strings.телефон }</td>
                            <td>
                                <button class="btnRedDel"  id="btnBack" on:click={()=>editBocks(index )}>
                                    ✎
                                </button>
                            </td>
                        </tr>
                    {/each}
                {/if}

                {#if visilbeSaerch}
                    {#each currentQues as strings, index}
                        <tr>
                            <td> {index +=1}</td>
                            <td> {strings.фио}</td>
                            <td> {strings.телефон }</td>
                            <td>
                                <button class="btnRedDel"  id="btnBack" on:click={()=>editBocks(index )}>
                                    ✎
                                </button>
                            </td>
                        </tr>
                    {/each}
                {/if}
                </tbody>

            </table>
        </section >
    </div>
</div>

{#if  !visible}
    <div class="newBocks">
        <div class="visibBocks">
            <button class="exit" on:click={visibleBocks}>&#10006;</button>
            <h3>Edit Bocks:</h3>
            <div class="inputColums">
                <label>
                    <p>ФИО</p>
                    <input type="text" name="Название" id=" "
                           on:input={(e)=>{
                    inputФио = e.target.value
                    console.log(inputФио)
                }}>
                </label>
                <label>
                    <p>Телефон</p>
                    <input type="text" name=">Имя автора" id=" "
                           on:input={(e)=>{
                    inputтелефон = e.target.value
                }}>
                </label>

                <button style="margin-top: .7em; padding:.2em"
                        on:click={saveBocks}>
                    Сохранить
                </button>
            </div>
        </div>
    </div>
{/if}

{#if  visibleRedaction}
    <div class="newBocks">
        <div class="visibBocks">
            <button class="exit" on:click={()=>visibleRedaction = !visibleRedaction }>&#10006;</button>
            <h3>Edit Bocks:</h3>
            <div class="inputColums">
                <label>
                    <p>ФИО</p>
                    <input type="text" name="Название" id=""
                           value={inputФиоRedackt}
                           on:input={(e)=>{
                    inputФиоRedackt = e.target.value
                    console.log(inputНазвание)
                }}>
                </label>
                <label>
                    <p>Телефон</p>
                    <input type="text" name=">Имя автора" id=""
                           value={inputтелефонRedackt}
                           on:input={(e)=>{
                    inputтелефонRedackt = e.target.value
                }}>
                </label>


                <button style="margin-top: .7em; padding:.2em"
                        on:click={()=>saveEditBocks(marker)}>
                    Сохранить
                </button>
            </div>
        </div>
    </div>
{/if}

<style>
    .newBocks{
        font-size: 1.2em;
        position: absolute;
        top: 0;
        /*opacity: .7;*/
        height: 100vh;
        width: 100%;
        background-color: rgba(58, 58, 58, 0.7);
    }
    .visibBocks{
        padding: 2em;
        margin: 20% auto;
        width: 400px;
        height: fit-content;
        /*background-color: #fff;*/
        background-color: #eeeeee;

    }
    .exit{
        border: none;
        margin-left: 98%;
        margin-top: -2em;
        /*position: absolute;*/
        cursor: pointer;
    }

    .inputColums{
        margin-top: 1em;
        display: flex;
        flex-direction: column;
    }
    .inputColums p{
        font-weight: 600;
        font-size: medium;
    }
    label{
        margin-top: .5em;
    }
    .visibBocks input{
        height: 1.7em;
        width: 100%;
        border: #bdbdbd solid 1px;
    }
</style>