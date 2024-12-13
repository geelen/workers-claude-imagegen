# Claude + Workers AI Image generation

An example of [`workers-mcp`](https://github.com/geelen/workers-mcp).

```ts
/**
 * Generate an image using the `flux-1-schnell` model. Works best with 8 steps.
 *
 * @param {string} prompt - A text description of the image you want to generate.
 * @param {number} steps - The number of diffusion steps; higher values can improve quality but take longer. Must be between 4 and 8, inclusive.
 * */
async generateImage(prompt: string, steps: number) {
  const response = await this.env.AI.run('@cf/black-forest-labs/flux-1-schnell', {
    prompt,
    steps,
  })
  // Convert from base64 string
  const binaryString = atob(response.image)
  // Create byte representation
  const img = Uint8Array.from(binaryString, (m) => m.codePointAt(0))
  return new Response(img, {
    headers: {
      'Content-Type': 'image/jpeg',
    },
  })
}
```

![image](https://github.com/user-attachments/assets/352867ad-6ae0-4046-88a7-a41684846e47)
