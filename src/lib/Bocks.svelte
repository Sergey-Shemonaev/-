<script>


    $: arrBocks =[
        {

            название: 'Божественная комедия',
            имяAвтора: 'А. Данте.',
            названиеИздательства: '&',
            годИздательства: '1582',
            колвоСтранц: '350',
            кличество: '1'
        },
        {

            название: 'Гамлет ',
            имяAвтора: 'У. Шекспир',
            названиеИздательства: '&',
            годИздательства: '465',
            колвоСтранц: '500',
            кличество: '1'
        },
        {

            название: 'Фауст',
            имяAвтора: 'И.-В. Гёте',
            названиеИздательства: '&',
            годИздательства: '1685',
            колвоСтранц: '100',
            кличество: '2'
        },
        {

            название: 'Мещанин во дворянстве ',
            имяAвтора: 'Ж.-Б. Мольер.',
            названиеИздательства: '&',
            годИздательства: '1598',
            колвоСтранц: '200',
            кличество: '3'
        },
        {

            название: 'Евгений Онегин',
            имяAвтора: 'А. С. Пушкин',
            названиеИздательства: '&',
            годИздательства: '1850',
            колвоСтранц: '520',
            кличество: '5'
        },
        {

            название: 'Герой нашего времени',
            имяAвтора: 'М. Ю. Лермонтов',
            названиеИздательства: '&',
            годИздательства: '1890',
            колвоСтранц: '410',
            кличество: '6'
        },
        {

            название: 'Ромео и Джульетта',
            имяAвтора: 'У. Шекспир',
            названиеИздательства: '&',
            годИздательства: '800',
            колвоСтранц: '459',
            кличество: '4'
        }
    ]
    $: sortStron = true;
    const sortArrs = (fieldName, повозраст) => {
        if(повозраст){
            arrBocks.sort((a, b)=>{
                if(a[fieldName] < b[fieldName]) return 1;
                else if (a[fieldName] > b[fieldName]) return -1;
                else  return 0;
            })

        }
        if(!повозраст){
            arrBocks.sort((a, b)=>{
                if(a[fieldName] < b[fieldName]) return -1;
                else if (a[fieldName] > b[fieldName]) return 1;
                else  return 0;
            })

        }
        arrBocks= [...arrBocks]
    }

    const sortOptions = [
        {
            title:'по названию',
            value: 'название'
        }, {

            title: 'по имени автора',
            value: 'имяAвтора'
        }, {
            title:'по количеству экземпляров',
            value: 'кличество'
        }
    ];
    let selected = sortOptions[0];
    $: console.log(selected);

    / Функция добавления в массив /
    $: visible =true;
    $: visibleRedaction = false;
    function visibleBocks() {
        visible = !visible
    };
    $: marker = 0;
    let inputНазваниеRedackt = '';
    let inputИмяАвтораRedackt = '';
    let inputГодИздательстваRedackt = '';
    let inputНазваниеИздательстваRedackt = '';
    let inputКолвоСтраницRedackt = '';
    let inputКолвоШтукRedackt = '';
    let inputНазвание = '';
    let inputИмяАвтора = '';
    let inputГодИздательства = '';
    let inputНазваниеИздательства = '';
    let inputКолвоСтраниц = '';
    let inputКолвоШтук = '';
    const saveBocks = ()=> {
        const newBocks = {
            название: inputНазвание,
            имяAвтора: inputИмяАвтора,
            названиеИздательства: inputГодИздательства,
            годИздательства: inputНазваниеИздательства,
            колвоСтранц: inputКолвоСтраниц,
            кличество: inputКолвоШтук
        }
        arrBocks = [...arrBocks, newBocks]
        visible = !visible
    };

    const editBocks =(id)=>{
        marker = id;
        console.log(id)
        inputНазваниеRedackt = arrBocks[marker].название
        inputИмяАвтораRedackt = arrBocks[marker].имяAвтора
        inputГодИздательстваRedackt = arrBocks[marker].годИздательства
        inputНазваниеИздательстваRedackt = arrBocks[marker].годИздательства
        inputКолвоСтраницRedackt = arrBocks[marker].колвоСтранц
        inputКолвоШтукRedackt = arrBocks[marker].кличество
        visibleRedaction = !visibleRedaction;
    }

    const saveEditBocks = (id) =>{
        arrBocks[id] ={
            название: inputНазваниеRedackt,
            имяAвтора: inputИмяАвтораRedackt,
            названиеИздательства: inputНазваниеИздательстваRedackt,
            годИздательства: inputГодИздательстваRedackt,
            колвоСтранц: inputКолвоСтраницRedackt,
            кличество: inputКолвоШтукRedackt
        }
        console.log(id)
        arrBocks = [...arrBocks]
        visibleRedaction = !visibleRedaction
    }

    const dell=(id)=>{
        arrBocks.splice(id, 1)
        arrBocks = [...arrBocks]
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
        coppy = arrBocks;
        currentQues = arrBocks.filter((el)=>el.название.toLocaleLowerCase().includes(inputSearch.toLocaleLowerCase()) && el !== inputSearch);
        console.log(currentQues)
        arrBocks = currentQues;
        searchButton = !searchButton;
        visilbeSaerch =!visilbeSaerch;
        visibleDock =!visibleDock;
    };
    const searchReset = () => {
        arrBocks = coppy;
        searchButton = !searchButton
        inputField.value = '';
        visilbeSaerch =!visilbeSaerch;
        visibleDock =!visibleDock;
    };


</script>

<div class="contenier">
    <div class="bocks">
        <section >
            <div class="allCards">
                <div>
                    <h4>Bocks</h4>
                </div>
                <div>
                    <button on:click={visibleBocks}>New card</button>
                </div>
            </div>
            <div class="space_betvin">
                <div>
                    <span>   сортировка по:</span>
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
        <section >
            <table>
                <thead>
                <tr>
                    <th colspan="1">ID</th>
                    <th colspan="1">название</th>
                    <th colspan="1">имя автора</th>
                    <th colspan="1"> год издательства</th>
                    <th colspan="1"> название издательства</th>
                    <th colspan="1">количество страниц</th>
                    <th colspan="1">количество экземпляров в библиотеке</th>
                    <th colspan="1">редактирование</th>
                </tr>
                </thead>
                <tbody>
                {#if visibleDock}
                    {#each arrBocks as strings, index }
                        <tr>
                            <td>{index +1 }</td>
                            <td> {strings.название}  </td>
                            <td> {strings.имяAвтора}</td>
                            <td>{strings.годИздательства} </td>
                            <td>{strings.названиеИздательства} </td>
                            <td> {strings.колвоСтранц}</td>
                            <td>{strings.кличество} </td>
                            <td>
                                <button class="btnRedDel" id="btnBack" on:click={()=>editBocks(index )} >
                                    ✎
                                </button>
                                <button class="btnRedDel" on:click={()=>dell(index)  } >Dell</button>
                            </td>
                        </tr>
                    {/each}
                {/if}
                {#if visilbeSaerch}
                    {#each currentQues as strings, index }
                        <tr>
                            <td>{index +1 }</td>
                            <td> {strings.название}  </td>
                            <td> {strings.имяAвтора}</td>
                            <td>{strings.годИздательства} </td>
                            <td>{strings.названиеИздательства} </td>
                            <td> {strings.колвоСтранц}</td>
                            <td>{strings.кличество} </td>
                            <td>
                                <button class="btnRedDel" id="btnBack" on:click={()=>editBocks(index )} >
                                    ✎
                                </button>
                                <button class="btnRedDel" on:click={()=>dell(index)  } >Dell</button>
                            </td>
                        </tr>
                    {/each}
                {/if}

                </tbody>

            </table>
        </section>
    </div>

</div>

{#if  !visible}
    <div class="newBocks">
        <div class="visibBocks">
            <button class="exit" on:click={visibleBocks}>&#10006;</button>
            <h3>Edit Bocks:</h3>
            <div class="inputColums">
                <label>
                    <p>Название</p>
                    <input type="text" name="Название" id=""
                           on:input={(e)=>{
                    inputНазвание = e.target.value
                    console.log(inputНазвание)
                }}>
                </label>
                <label>
                    <p>Имя автора</p>
                    <input type="text" name=">Имя автора" id=""
                           on:input={(e)=>{
                    inputИмяАвтора = e.target.value
                }}>
                </label>
                <label>
                    <p>Год издательства</p>
                    <input type="text" name="Год издательства" id=""
                           on:input={(e)=>{
                    inputГодИздательства =e.target.value
                }}>
                </label>
                <label>
                    <p>Название издательства</p>
                    <input type="text" name="Название издательства" id=""
                           on:input={(e)=>{
                    inputНазваниеИздательства = e.target.value
                }}>
                </label>
                <label>
                    <p>Количество страниц</p>
                    <input type="text" name="Количество страниц" id="" on:input={(e)=>{
                    inputКолвоСтраниц = e.target.value
                }}>
                </label>
                <label>
                    <p>Колтчество штук в библиотеке</p>
                    <input type="text" name="Колтчество штук в библиотеке" id=""
                           on:input={(e)=>{
                    inputКолвоШтук = e.target.value
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
                    <p>Название</p>
                    <input type="text" name="Название" id=""
                           value={inputНазваниеRedackt}
                           on:input={(e)=>{
                    inputНазваниеRedackt = e.target.value
                    console.log(inputНазвание)
                }}>
                </label>
                <label>
                    <p>Имя автора</p>
                    <input type="text" name=">Имя автора" id=""
                           value={inputИмяАвтораRedackt}
                           on:input={(e)=>{
                    inputИмяАвтораRedackt = e.target.value
                }}>
                </label>
                <label>
                    <p>Год издательства</p>
                    <input type="text" name="Год издательства" id=""
                           value={inputГодИздательстваRedackt}
                           on:input={(e)=>{
                    inputГодИздательстваRedackt =e.target.value
                }}>
                </label>
                <label>
                    <p>Название издательства</p>
                    <input type="text" name="Название издательства" id=""
                           value={inputНазваниеИздательстваRedackt}
                           on:input={(e)=>{
                    inputНазваниеИздательстваRedackt = e.target.value
                }}>
                </label>
                <label>
                    <p>Количество страниц</p>
                    <input type="text" name="Количество страниц" id=""
                           value={inputКолвоСтраницRedackt}
                           on:input={(e)=>{
                    inputКолвоСтраницRedackt = e.target.value
                }}>
                </label>
                <label>
                    <p>Колтчество штук в библиотеке</p>
                    <input type="text" name="Колтчество штук в библиотеке" id=""
                           value={inputКолвоШтукRedackt}
                           on:input={(e)=>{
                    inputКолвоШтукRedackt = e.target.value
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