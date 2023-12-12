<script lang="ts">
    import type { Task } from "../lib/index";

    let progressTasks: Task[] = []
    let completedTasks: Task[] = []
    let placeholder: Task = {name: "Type Name Here", desc: "Type Description Here", done: false}
    let parrot = false

    function addItem () {
        if (placeholder.name != "" && placeholder.desc != "") {
            progressTasks.push({name: placeholder.name, desc: placeholder.desc, done: false})

            placeholder.desc = ""
            placeholder.name = ""
            progressTasks = progressTasks
            completedTasks = completedTasks
        }
            let notEmptyProgress = progressTasks.filter((notEmpty) => notEmpty.name != null)
            progressTasks = notEmptyProgress

            let notEmptyCompleted = completedTasks.filter((notEmpty) => notEmpty.name != null)
            completedTasks = notEmptyCompleted    }

    function completeItem (index : number) {
        progressTasks.forEach(task => {
        if (task.done == true) {
            completedTasks[completedTasks.length + 1] = progressTasks[index]
            progressTasks.splice(index, 1)

            let notEmptyProgress = progressTasks.filter((notEmpty) => notEmpty.name != null, undefined)
            progressTasks = notEmptyProgress

            let notEmptyCompleted = completedTasks.filter((notEmpty) => notEmpty.name != null, undefined)
            completedTasks = notEmptyCompleted
    }})
            progressTasks = progressTasks
            completedTasks = completedTasks
    }

    function uncompleteItem (index : number) {
        completedTasks.forEach(task => {
        if (task.done == false) {
            progressTasks[completedTasks.length + 1] = completedTasks[index]
            completedTasks.splice(index, 1)

            let notEmptyProgress = progressTasks.filter((notEmpty) => notEmpty.name != null, undefined)
            progressTasks = notEmptyProgress

            let notEmptyCompleted = completedTasks.filter((notEmpty) => notEmpty.name != null, undefined)
            completedTasks = notEmptyCompleted
    }})
            progressTasks = progressTasks
            completedTasks = completedTasks
    }

    function onKeyDown(e : any) {
		 switch(e.keyCode) {
            case 186: partyParrot()
         }}

    function partyParrot () {
        if (parrot == false) {
            parrot = true
        } else {
            parrot = false
        }}
</script>

<svelte:window on:keydown={onKeyDown}/>

<h1 id="title">To Do:</h1>

<div class="list">
    Incomplete Items:

    <button class="wasteOfSpace"></button>

    {#each progressTasks as task, index}
            <input bind:checked={task.done} type="checkbox"> <button on:click={() => completeItem(index)}>{task.name} - {task.desc}</button>
    {/each}
</div>

<div id="allInputs">
    <input class="input" bind:value={placeholder.name}>

    <input class="input" bind:value={placeholder.desc}>

    <button class="input" on:click={addItem}>Add new task (or click `)</button>
</div>  

<p class="list">
    Completed Items:

    <button class="wasteOfSpace"></button>

    {#each completedTasks as task, index}
            <input bind:checked={task.done} type="checkbox"> <button on:click={() => uncompleteItem(index)}>{task.name} - {task.desc}</button>
    {/each}
</p>

<div id="allImages">
    {#if parrot == true}
        <img  alt="Party Parrot" class="image" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAA6lBMVEX/////jYsAAAAAAQB7jGj6ioplNjhMIyT/j43CwsIwMDD09PRhYWH+jIvc3Nz/kY/IyMioqKhUVFTl5eXyhIRZWVnTdHUYDQ20Y2OAgIA/Pz/deXqGhoblf35KSkq6ZWYYGBibVVSESEhXMDBseVxyhGVHJygpFxY4Hx2TUU5rOzgTFA+lWllNKihnODkgEhNubm6fn580HR2ISkp2QEAAAAghISEzOy4lKR4bIBhDSzhoc1cZEA9KUz4vExK5ublsMjJaZk4VGhJIUDwtNCjIbWtRXkgjJx8YAAAoDw4sGhgeFBIgCg5LHBv9JwWEAAAQkUlEQVR4nO1dC3uTShq2E4kYS9PqFKgUEWi4JIQo0FZ781RLrd3d//93lvlmyBViyIWku/Oec3zO0zSRl3f47jN59YqDg4ODg4ODg4ODg4ODg4ODg4ODg4ODg4ODg4ODg4ODg4ODg4ODg4ODg4ODg4ODg4ODg4ODg4ODg4ODg4ODg4OD4/8YP94W4ce2L2steEfwARUje3Xb17cyvlAqjWJkr7xsHQ8OMvEaGb3yP9CnDwfZr237SpfE13HxCtbo6OfH277UZXD49vDjxOJUXDfyPM/J/o0id6CML9ZPh2/fvjgdL9BwgVJEdphYse+bppl0bWdwTnUc/srRtq+4Cg6/Hh1d5AKigevYSWyagWEYKcAwgiAj2g1ddygz+nL0glQ8pU8Zk++Pk8SyLk5jb08NvLuRkAi93fZ1L4rD00+I2ZAGskPVSGUN471Z6HqaqnEYMaOD9k9PDrd98QvhiF1wAz25buJjTBWbRfZjSTdMO1KU/Ja8hIfx4PgjYj7ACdNMPEkqYpdDwFiXQ5t5D/Tx+GDbBP6GwxNQEKFnr2mZmlCs3oSQEjYt21PY+3Z9oX6Ahy+Dkph70nz5RpCwFrsKWJzsrTttUg+/IPoE2t0gXYwdXavZ49j02NP4ZZdVPEIsDvPVvy7PqbXaNkMFsZW6bRqlOGRGRkkCTa/Cj0DSUr+rUM/4fldVPGQSIGJhqjLcEwU1zj3jbqp48PmCGIrGeSLrC1qYKQhYjs/PwVR93kWn8YEqqLiJjicVFAQJQISar6JmRgP6MbtnUN/l68tJ9ZGRIVFLqlpWYtv9MDZVDe/NtUCigJNMxZ1cqMAwe4xsSx4ZGUnXtFQ1k+Qfu98n+YWRajoW5i7UIHF31NxQCZUgHRqZTBC/O53WO3GK2/OWKtacnXQaWTpIbrxnyzi3MoJsmKEzzKNoMqVETSu7CXNVNMwBxDeo9WnbtMbA7rqT6CMFVWu2zEZ+0E/+omKau/7WtmmNgQVrAc7XqCQbUZRHOBPVJzSIrGDanUwkWFg2QfTsvbvzLLJ4O8A4cw2w2IyA5u4ZejnobUAN2xcmKEqSQMB+JmItUBRquXalCHdAzUzUtPuOHRtEDsFxqXFtfLt6vL8+y3B/e/mTqog8Mx1JRhyK03cSM68DiHu6YdN1ur9tagwH1JK4thO5UWJmHl/XIniY0OXlLSHY6XTOru8fry6/98hvRtltGLMtqh89u2N+RtTlxAO53+9IbHMAllJhz1yUpG3VJ6kQ6qHO2etxdC5/E96KZw6NjSiDZcnsbN/PH0axHSSNXXIZI4bkoty+KpkJMLz61elMMry+7RGnMRg9ie0gpimF4lnDeE/UZOeOrv1dKN28O0CMHHN7JrZsYHh//Xoa9z97RLCMDKPYTry89NhMR85GCt/QpP/i1db7U+9ynzesAVtp6ADZ684Mw+ur3+SVrjyUq/vE3okcXx49nlqKFLpQ3+8Ew4meUqLaUARFZzMEX5/9+kZeCQ0mlyB1h+VjLxkzsXu6R8XdvkF9N6z/5ho2TVI6Q71eEcPHB3LZoUoZili3h9pH9piJFYXM8QPFnWCIGoPBkCKyzYjo1PtezrAZFDFsjjEk5Sn7GUFnass+4x0ENFE06iQxht+/FTG8f4Bqf6Dl8V13GJdHoTGRPepGSKuTJ9tmSNaobStDLULTIz/7dlnAsHMPGtqmNrQ0Q0vlWePPIdE3jmCdHh9tV0W4zUkyGDaRwoDYCPRwNWtKgWH2Wn9oNtvdQW5pHFOerAC0g5DVib9ukd/JCbjrQO32qelToiQADS9vixheX4KGI4Y0OmigczRT4SHRH/W02/T7rABlyFDuzOCFMWP4WM6wH+cMRSNwFciOnXimRidJtgeff7LFZUoTp4Eu4LTvkv+zdMMCS3NV4PCBYfaaYw0XpIBp78lJtWmCGX812HoeBbd44GXGX/etsJvEqpBaEUSlhQzPQEMnkUcBWuAnYZj4WkEblcTlA+i7HW0tGwYNPRvcG9Y1TciuKp6j4RnVsDtuVASspbi4zChhx9myywANmzFhKAoYZwG1KPteuYYdquEEQwljvaQRMCz2o9OtMkwCKgGUW4YM7xdluDevUCwYW2X4ZR/+9kAbqxCKcuBAfl9oSztX5DXPlss5Ta1TLQBL1DreygwcHZtBqj7BUHXKvUXGEILshRmKetqlT+JWnGILPNnNZLSlGVTDIo//+jVoeNdfmGH2gYEN9vTiYgv2tEUroLMMy2IawjB77W5xDbOwhzrYxlaGilpTzo0uK7lPflwcl54VWpr5yIICGvPWruG74x5ZpaNUaMSwNPJm/jCpwlDCVh96GR/rjsDf07XTlfXJrEezQcPLktxiIi5dBKKUh+eo5vh0nwal1mSRXsSYlKyz/LCAIcnx0aiKsaiIenoHZaD6GZLbeh5P9pKAYfbC70KGt9+gimFUYpjl++5W2t/AUOkGM92yJnmhsIpxffmdvJZoJXFoCURsJmygqGaGpESfVGWYvcmqzBDakWTJ1FkgputmkGrTF9sOz+GhKWL48JNcZ1yFHkWK6AxDjQRf0RqKq808Um3SOiIMC2rev6GqvwzDJsTz6HONTpE+GO7sfFA7tqEwUZBcQN+icW7ObXQXQdRM1lSsMbChi9QpYBjE0Jm5fZxlCMUqdwmGWGeJYp0MiU5uf9ZkiIYJGl79mmUIrcKoOsMMbEjjR322BjR8ExYw1GRIBh4epgl2Hsk1DuxZ87uAimns1RzYgIZ2UsBQJw4aod/fpxme3ZI3ueFSDEneWW9gQwsYcZFjkyJyJT00LeEtxN0TffzFIQkhtTX1MozNotsNsxjZP9MMryAqdYIqcffYp7Je41FdxgZWaaAWXYzQhAQKTffxH3rQeZp1oYsxJM2R+gKbH7A1Bhly0cVIMYSR0538s98kkb0J5w4olkOI+2zcvRaGF7QrJM/EbMAw8EHDSY/YuYaZoedk/ihtKSQYd69Nwxa13NP9InYtsgEvX15NOMNfpCagNP3lxqT3JDUe1KghY1i0ZyuDLsPN/jbB8PYStkPNTu4tytAw6X4+9KOO2mmLrtKyfoMO6X/vcpzhZQ/6VIa2LENZdfN2aj0MG+UMRez+IbfgYWRNO2fgKlxnNGZbFXoa5S3xehjO0VDEfQhAvj9ej55CSH695lKuglH0dkjDIIHhvcv7nOHjN6g9WkG19H6aYa0azmG4J6QmBJG9ob/4BeNvyJSXc4YEYt0MUbktzYJIlSY7rI14dgVFtoE7d5D9LxC04Srd33xJqkXttl52wW2jT2wNuqSZ/v0DFNkqtNUKgLVcQzK0WAPD8phmjySJgU1+4fvDWUbw+hf99aSsnb0IJM2I8jnBGib56cwkmq205Qx1uUlW6c/fZ50s84WWkxIVziMszFBWo6GGn082H9iAqSnOLSiscwgirzudM8gp0HNiVNt6Oc0wcKl9a9QTnMJF+0HpBYlmAmvq9v4Rhp+RYqeVt15OMCRRGxv0q4dhaQZM0Q5iRJtQDzA2ixrdFexoBoFG3rnDqEnDZkGdhkHE+AmC014PFlakysuGa4yhGd7AYBmES3VpWFSJyoGFp3M2sEj+89JlQ24KEfJDMsRIhwQ3TpAyfPLE8stud/9BQ8OQrBKuAXAIe6eeApX1SzfOEAYxvDm6tP04j0GUgb+KKwSCOrifQWQYdEdOHQxJ30IvzxVELaUTwFlW6Mjt1QiKKZ09dpo6Zv3STTN8fwH5Xloeh4lY+/OHBtwV+9pFH2Z0wVdkqx03nVo0pD3gQTCnvCti746ORsdL1tdGH9U26aitmQo4sevpJdIud0EPeIwh3UoamVXOySgE1uCTFMUQJEFW2T6kjTMkpTN7TiNJEgwfdjirq6QUBCJOE7Azz2k7y6IMevxSa8O7ovbpjHc8r80iGYrSsKcGUpZAW4aR73wfg8YGwDe8K4qOXiJr3kE0Yuq4ytL1wyEkbNBtqdRiibpl17Er6pg+DHNHR7I0se+uamXItEmXdtbYBICAA/qXb5bh0elnuK3zxn9EPQ38lRliDawncpv5asCBA530Te+KgvnSN/58M6KtUHtikNUBHZn380HPtpHQBt6GR9xh+jJqpnMZCiuk9RSS37whTjXq6sMd37pms3ipt2GGWUDmzWe4MiAghQzaH430SwLsryUu48MGp91AQwWly4xWLA61+0y3AMoTJYJ0GPRu0GW0aOaQruzuyiFgLfZoWpiMbwnIrLT2TIuLmzSorE06sRthrRD3hMyh0lzJlKceaNJp3rRTPKIHmJnpysakhCDWg1gBBSPbmOlZpWoEYcDHo6OvG3MacHctddX0vYyhJqMnelaD489WZkXddvJj/ja2GwM07JobYSjqehIiUNANTb1gnQhyPGBHLh5vao8iLUdZq6a3RciSpPQPlch1zBJ7bdh3N8yinm6GIlyAE66dobiH5ThL5el5Ir5aFvhhbDkNtlu4sRG/CBqy/YdrhKTrmmrf0QGhfmjIUulfoFoOO48YnR59XT9JGi7218pQFMlAzs1NbkTmH54lCVaYHwawiY1DoGHkrJGhRE4YNpIuooVkxY7/ck6hlKpdJy/175+sW0U03Ae8FohiOzOQQf9fKBcQxX+d629jNcnPFVv/Ea+0LByth6Ek6XJgWon9rFDTgbpWqv19OEXCcmCfM4Pzfn9/rXEqLdW4KzKE3bXk8ZNVeowdO70AWlsLfHSWZ+cnvILwa2W4Dg1FXVaJdA45cZ+WCUk26KSatGjAK2Eo3TC/0WqtL2mkGq72HEqCZphx144GjfycPnT+7//YiVwlVMJm0mdnSpOPWZvFWd0fSjg9b4yfygdwm7LertQSF9uSToo3w8W6LoZQqVklppE042mAxr7VoxH1rdhUi+c650HQ08DqRvnB2ZnFWUe9GDRsrhKXSoaJWEzC0E9STawmIEXma2Cgn6309RynARom5ioMZZWFlY0b17H9QNbIafVLfhrW5dRqsmgB9VqrnxGKxs9UWI4hbUIAbpymKpd91cBCyGTU6cmwbFWsOFnExobU0tmvhYA1ww9UWRfGz8BcARLWfHtEciX/36KRh7FSUVskzkI1NH1vFfEmPlA3ExdcD63irGBwaDXRXbWamC2t9prYsQ9st1P1ZpCruEJZvEVrRBuuCC8DUZNN6w0r/H85WFpFeqZCpc31dSFbEnLi5CouWadiJ+mH6SaqNGsA1gLr38zVtpZS8Zg+ycnKzbMNQWyngZdH8ksl//TEgbvZU8h2BhirARNxSYZQaFtqy2tNEGXDpeZmqW/MotMm/lLbJeuCJNAp18YyLuPtJ5gYMnbRko4gpTBp1ED71b+9jpaK3NVbvJuFKNsRWu58SZr89hcuNGwJMGsEmWdFp0i/oBLZBbvVdw4mVH+qMvxMo4U5k+y7AzWJlmDIGtzqyiN5m4comzCteVLN1rRoSbp6NaV+iGSYA662ktsHDV1lxw0phYTZ19dUZUim5pf48qotQCLnyVQLTtlIW+LvuKtgkAL6XQYVGLK0wjdeCEO226YCw31adU2XrvrVCnEvDWAKvsIJTDRxQin9ipjdRwq73qp8RSbVULHD5suA3Wcd1wXnNX6ctmh/z3vzQuBErGKzIMOTUS/y5aBRheFpvs/xxf2xOMPGCwXX8H9Ow/8CE6fbA6xacMsAAAAASUVORK5CYII=">
    {/if}

    {#if parrot == true}
        <img  alt="Party Parrot" class="image" src="data:image/png;base64,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">
    {/if}

    {#if parrot == true}
        <img  alt="Party Parrot" class="image" src="data:image/png;base64,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">
    {/if}
</div>

<style>
    :global(body) {
        background-color: rgb(120, 141, 141);
        color: rgb(0, 0, 0);
    }

    .image {
        scale: 0.7;
        border: 5px solid rgb(0, 0, 0);
        display: inline-grid;
        width: 90%;
    }

    #title {
        display: grid;
        place-content: center;
        font-size: 55px;
    }

    #allImages {
        display: grid;
        grid-template-columns: auto auto auto;
        border: 5px solid rgb(0, 0, 0);
        background-image: radial-gradient(#707070 25%,#FCFCFC);
        padding: 15px;
        margin: 15px 40px;
        border-radius: 7px;
        width: 1385px;
    }

    .input {
        border: 5px solid rgb(0, 0, 0);
        background-image: radial-gradient(#707070 25%,#FCFCFC);
        padding: 15px 0px;
        text-align: center;
        display: inline-grid;
        font-size: 20px;
        cursor: pointer;
        width: 90%;
        border-radius: 7px;
    }

    #allInputs {
        display: grid;
        grid-template-columns: auto auto auto;
        place-items: center;
        margin: 0px 15px;
    }

    .list {
        display: grid;
        grid-template-columns: max-content max-content;
        border: 5px solid rgb(0, 0, 0);
        background-image: radial-gradient(#707070 25%,#FCFCFC);
        padding: 15px;
        margin: 15px 40px;
        border-radius: 7px;
        width: 1385px;
        font-size: 20px;
        font-family: arial;
    }

    .wasteOfSpace {
        opacity: 0%;
    }
</style>
