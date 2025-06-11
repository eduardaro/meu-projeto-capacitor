<script>
    let display = $state('');

    function clear() {
        display = '';
    }

    function calc() {
       display = eval(display)
    }

    function press(c) {
        display += c;
    }

    function backspace() {
        display = display.length > 1 ? display.slice(0, -1) : '';
    }

    function round() {
    
    const val = eval(display);
    display = Math.round(val);

    }

    function log10() {
         const val = eval(display);
         display = Math.log10(val);
    }

    function sqrt() {
        const val = eval(display);
        display = Math.sqrt(val);
    }

    function percent() {
        display += '%';
    }

    function square() {
        const val =eval(display);
        display = val * val;

    }


    function invert(){
        display = eval(display) * -1;
    }
</script>

<div class="text-center mt-3">
<input class="form-control form-control-lg" readonly bind:value={display}>    
<table class="table table-borderless">
    <tbody>
    <tr>
        <td><button type="button" class="btn btn-danger w-100" onclick={() => clear()}>C</button></td>
        <td><button type="button" class="btn btn-dark w-100" onclick={() => press('(')}>&lpar;</button></td>
        <td><button type="button" class="btn btn-dark w-100" onclick={() => press(')')}>&rpar;</button></td>
        <td><button type="button" class="btn btn-info w-100" onclick={() => press('/')}>/</button></td>
    </tr>

    <tr>
        <td><button class="btn btn-info w-100" onclick={() => sqrt()}>√</button></td>
        <td><button class="btn btn-info w-100" onclick={() => square()}>x²</button></td>
        <td><button class="btn btn-info w-100" onclick={() => log10()}>log10</button></td>
        <td><button class="btn btn-info w-100" onclick={() => press('%')}>%</button></td>

    </tr>

    <tr>
    <td><button class="btn btn-info w-100" onclick={() => invert()}>±</button></td>
    <td><button class="btn btn-info w-100" onclick={round}>⭮</button></td>
    <td><button class="btn btn-info w-100" onclick={() => modulo()}>mod</button></td>
    <td><button class="btn btn-info w-100" onclick={() => press('*')}>x</button></td>
</tr>

    <tr>
        <td><button type="button" class="btn btn-dark w-100" onclick={() => press('7')}>7</button></td>
        <td><button type="button" class="btn btn-dark w-100" onclick={() => press('8')}>8</button></td>
        <td><button type="button" class="btn btn-dark w-100" onclick={() => press('9')}>9</button></td>
        <td><button type="button" class="btn btn-info w-100" onclick={() => press('*')}>x</button></td>
    </tr>
    <tr>
        <td><button type="button" class="btn btn-dark w-100" onclick={() => press('4')}>4</button></td>
        <td><button type="button" class="btn btn-dark w-100" onclick={() => press('5')}>5</button></td>
        <td><button type="button" class="btn btn-dark w-100" onclick={() => press('6')}>6</button></td>
        <td><button type="button" class="btn btn-info w-100" onclick={() => press('-')}>-</button></td>
    </tr>
    <tr>
        <td><button type="button" class="btn btn-dark w-100" onclick={() => press('1')}>1</button></td>
        <td><button type="button" class="btn btn-dark w-100" onclick={() => press('2')}>2</button></td>
        <td><button type="button" class="btn btn-dark w-100" onclick={() => press('3')}>3</button></td>
        <td >
            <button type="button"  class="btn btn-info w-100 " onclick={() => press('+')}>+</button></td>
    </tr>
    <tr>
        <td><button type="button" class="btn btn-dark w-100" onclick={() => press('0')}>0</button></td>
        <td><button type="button" class="btn btn-info w-100" onclick={() => press('.')}>.</button></td>
        <td><button type="button" class="btn btn-info w-100" onclick={() => calc('=')}>=</button></td>
        <td><button class="btn btn-danger w-100" onclick={() => backspace()}>⌫</button></td>
    </tr>
    </tbody>
</table>
</div>
