---
name: lianbu
description: Create face-focused image-generation workflows from a full-body model photo. Use when the user provides a model/person image and wants the face cropped or isolated, converted into front/three-quarter/profile face views, then redrawn in a high-quality colored-pencil hand-drawn style while preserving recognizable facial structure.
---

# Lianbu

## Workflow

Use this skill when the user provides a full-body or upper-body model image and asks for a face three-view reference sheet followed by a colored-pencil style redraw.

1. Confirm there is exactly one intended model image. If the image is missing, ask for it.
2. Extract or crop the face region first. Include the full head, hairline, ears when visible, chin, and a small margin around the face. Avoid including the full body unless the face is too small to crop reliably.
3. Generate a neutral three-view face sheet from the face crop:
   - front view
   - three-quarter view
   - side profile view
4. Redraw the generated three-view sheet with the required style prompt.
5. Verify the final result before responding: three distinct views are present, identity cues remain consistent, the face is clear, the background is white, and the result reads as colored-pencil hand drawing rather than a photo filter.

## Generation Prompts

For the three-view generation step, adapt this prompt to the available image-generation tool:

```text
Using the provided cropped face as the identity reference, create a clean face reference sheet with three views of the same person: front view, three-quarter view, and side profile view. Preserve the person's recognizable facial proportions, hairstyle, face shape, eyes, nose, mouth, and overall identity. Show only the head and neck area. Use a white background, clear lighting, high resolution, and a neat character reference layout. Do not add accessories or change the person's age, gender presentation, ethnicity, or expression beyond a neutral natural expression.
```

For the style redraw step, use the user's required prompt exactly, adding only preservation constraints if needed:

```text
将图像中人物脸部转换为高质量彩铅手绘风格，脸部保持手绘感但五官结构准确可辨，整体温暖艺术氛围，白色背景，清晰高分辨率。
```

If the tool benefits from a fuller prompt, append:

```text
保持三视图构图不变，保持同一人物身份特征一致，避免照片质感、油画质感、漫画夸张变形和复杂背景。
```

## Tool Guidance

- Prefer an image editing or generation tool that can use the uploaded image as a visual reference.
- If the user uploads a new image in the same turn, use that image rather than an older image from the conversation.
- When cropping is not available as a dedicated tool, produce a face-only intermediate image with the available image editor or ask for a closer face crop if the original image is too low-resolution.
- Do not skip the face crop. The crop is the identity anchor for the three-view generation.
- Do not generate the colored-pencil version directly from the full-body image; first create the three-view sheet, then restyle that sheet.

## Response Format

Keep the response short:

- State that the face was isolated, the three-view sheet was generated, and the colored-pencil redraw was applied.
- Mention any limitation that remains visible, such as low source resolution, occluded face, extreme pose, or weak side-profile consistency.
- Show or link the final image artifact when the environment supports it.
