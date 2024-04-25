<script lang="ts">
let customPromptInput: string = '';
let customInputName: string = '';
let customInputs: {
    name: string,
    value: string
} [] = [];
let overallTopic: string = '';
let audience: string = '';
let thesisStatement: string = '';
let bodyTopic1: string = '';
let bodyTopic2: string = '';
let bodyTopic3: string = '';
let mainConcludingPoint: string = '';
let combinedPrompt: string = '';

let prompts: string[] = [
    'You are a teacher evaluating an essay on the topic of {overallTopic}. Using the guidance below, respond to the student\'s work with constructive feedback, using concise headings and dot points',
    'Evaluate the clarity and strength of the thesis statement: {thesisStatement}. Is it compelling and clearly linked to the overall topic ({overallTopic})?',
    'Analyze the relevance of the topic discussed in body paragraph 1: {bodyTopic1}. Does it effectively support the thesis with adequate evidence?',
    'Review the argument and evidence provided in body paragraph 2: {bodyTopic2}. How well does it reinforce the thesis?',
    'Assess the effectiveness of the content in body paragraph 3: {bodyTopic3}. Does it provide new insights or repeat previous points?',
    'Evaluate the integration and flow among all body paragraphs. Does each paragraph smoothly transition to the next while maintaining coherence?',
    'Analyze the effectiveness of the concluding paragraph: {mainConcludingPoint}. Does it effectively summarize the essay and reinforce the thesis without introducing new information?',
    'Assess how the essay addresses the intended audience: {audience}. Is the language and tone appropriate for their understanding?'
];

let selectedPrompts: boolean[] = Array(prompts.length).fill(false);

function addCustomPrompt(): void {
    if (customPromptInput.trim() !== '') {
        prompts = [...prompts, customPromptInput];
        selectedPrompts = [...selectedPrompts, false]; // Extend the array to include the new prompt
        customPromptInput = ''; // Clear the input field after adding
    }
}

function addCustomInput(): void {
    if (customInputName.trim() !== '') {
        customInputs = [...customInputs, {
            name: customInputName,
            value: ''
        }];
        customInputName = ''; // Clear the input name field after adding
    }
}

function updateCustomInputValue(index: number, newValue: string): void {
    const updatedInputs = customInputs.map((input, idx) => {
        if (idx === index) {
            return {
                ...input,
                value: newValue
            };
        }
        return input;
    });
    customInputs = updatedInputs;
}

function togglePrompt(index: number): void {
    const newPrompts = [...selectedPrompts];
    newPrompts[index] = !newPrompts[index];
    selectedPrompts = newPrompts;
}

function fillSampleData(): void {
    overallTopic = 'Critique of the TEEL Paragraph Structure in Academic Writing';
    audience = 'Educators and advanced students of English and writing';
    thesisStatement = 'While the TEEL structure aims to scaffold student writing, it often restricts creative thought and undermines the complexity of effective writing.';
    bodyTopic1 = 'The historical critique of formulaic writing structures and their impact on students with varying skill levels.';
    bodyTopic2 = 'The limitations of TEEL in fostering writing innovation and intellectual engagement among students.';
    bodyTopic3 = 'Comparative analysis of expert opinions on the efficacy of formulaic writing models versus organic, flexible writing strategies.';
    mainConcludingPoint = 'Educational strategies should evolve beyond rigid formulas to embrace more dynamic, student-centered approaches to teaching writing.';
}

// Reactive statement to include custom inputs in combinedPrompt
$: {
    combinedPrompt = prompts.map(prompt => {
        let updatedPrompt = prompt;
        customInputs.forEach(input => {
            const regex = new RegExp(`{${input.name}}`, 'g');
            updatedPrompt = updatedPrompt.replace(regex, input.value);
        });
        return updatedPrompt;
    }).join('\n');
}

function handleInput(event: Event, index: number): void {
    const target = event.target as HTMLInputElement; // Safely assert here
    if (target) {
        updateCustomInputValue(index, target.value);
    }
}
</script>

      <style>
textarea {
    width: 100%;
    height: 200px;
    padding: 10px;
    font-size: 16px;
    border: 1px solid #ccc;
    border-radius: 5px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    resize: vertical;
}

div {
    margin-bottom: 10px;
}

input[type="text"] {
    width: 100%;
    padding: 10px;
    font-size: 16px;
    border: 1px solid #ccc;
    border-radius: 5px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}
</style>

<div>
    <h1>AI Essay Feedback Tool</h1>
    <button on:click={fillSampleData}>Load Sample TEEL Essay Data</button>

    <h2>Inputs</h2>

    <div>
        <label for="overallTopic">Overall Topic / Question:</label>
        <input id="overallTopic" type="text" bind:value={overallTopic} placeholder="Enter the overall topic or question">
    </div>

    <div>
        <label for="audience">Audience:</label>
        <input id="audience" type="text" bind:value={audience} placeholder="Describe the target audience">
    </div>

    <div>
        <label for="thesisStatement">Thesis Statement / Ideas:</label>
        <input id="thesisStatement" type="text" bind:value={thesisStatement} placeholder="Enter the thesis statement">
    </div>

    <div>
        <label for="bodyTopic1">Topic for Body Paragraph 1:</label>
        <input id="bodyTopic1" type="text" bind:value={bodyTopic1} placeholder="Enter topic for body paragraph 1">
    </div>

    <div>
        <label for="bodyTopic2">Topic for Body Paragraph 2:</label>
        <input id="bodyTopic2" type="text" bind:value={bodyTopic2} placeholder="Enter topic for body paragraph 2">
    </div>

    <div>
        <label for="bodyTopic3">Topic for Body Paragraph 3:</label>
        <input id="bodyTopic3" type="text" bind:value={bodyTopic3} placeholder="Enter topic for body paragraph 3">
    </div>

    <div>
        <label for="mainConcludingPoint">Main Concluding Point:</label>
        <input id="mainConcludingPoint" type="text" bind:value={mainConcludingPoint} placeholder="Enter the main concluding point">
    </div>

    {#each customInputs as input, index}
    <div>
        <label for="{input.name}">{input.name}:</label>
        <input
            id="{input.name}"
            type="text"
            bind:value={input.value}
            on:input={(event) => handleInput(event, index)}
        placeholder={`Enter value for ${input.name}`} />
</div>
{/each}

<h2>Custom prompts and inputs</h2>

<div>
    <input type="text" bind:value={customPromptInput} placeholder="Enter your custom prompt here" />
    <button on:click={addCustomPrompt}>Add Custom Prompt</button>
</div>

<div>
    <input type="text" bind:value={customInputName} placeholder="Enter name for custom input" />
    <button on:click={addCustomInput}>Add Custom Input</button>
</div>

<fieldset>
    <legend>Select feedback prompts:</legend>
    {#each prompts as prompt, index}
    <label>
        <input
            type="checkbox"
            on:change={() => togglePrompt(index)}>
        {prompt}
    </label><br>
    {/each}
</fieldset>

<div>
    <label for="customPrompt">Your Combined Prompts:</label>
    <textarea id="customPrompt" placeholder="Your combined prompts will appear here..." readonly>{combinedPrompt}</textarea>
</div>

<p>Copy the above prompts and your essay text, then paste them into the AI interface of your choice.</p>
</div>
