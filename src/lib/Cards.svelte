<script>

    $: dates= new Date().toLocaleDateString()
    let visible = true;


</script>


<div class="contenier">
    <contanier id="cards" >
        <section>
            <div class="allCards">
                <div>
                    <h4>ALL VISITORS</h4>
                </div>
                <div>
                    <button>New visitior</button>
                </div>
            </div>
            <div class="space_betvin">
                <div>
                    <span>   сортировка по:</span>
                    <select>
                        <option>ID</option>
                        <option>по имени автора</option>
                        <option>по количеству экземпляров</option>
                    </select>
                    <button>Sort</button>
                </div>
                <div>
                    <span>Поиск</span>
                    <input type="text" name="" id="">
                    <button>Поиск</button>
                </div>
            </div>
        </section>
        <section>
            <table>
                <thead>
                <tr>
                    <th style="width: 10%">ID</th>
                    <th style="width: 22.5%">Id посетителя</th>
                    <th style="width: 22.5%">Id книги</th>
                    <th style="width: 22.5%">дата, когда взял книгу</th>
                    <th style="width: 22.5%">дата, когда вернул книгу</th>
                </tr>
                </thead>
                <tbody>
                <tr>
                    <td> 12</td>
                    <td> 5</td>
                    <td> 6</td>
                    <td> {dates}</td>

                    <td>
                        {#if visible}
                            <button class="btnRedDel" on:click={()=>{visible = !visible}}  >
                                &#8634;
                            </button>
                        {/if}
                        {#if !visible}
                            <p on:click={()=>{visible = !visible}} >{dates}</p>
                        {/if}
                    </td>
                </tr>
                </tbody>

            </table>
        </section >

    </contanier>
</div>