# Social-Card: Dynamic Image Creation on the Edge with Vercel Open Graph

> A dynamic image generator for business, profile, and social cards using Vercel Open Graph, Next.js, and TailwindCSS. Easily customize and create visually appealing cards for any purpose.

Author: Senthilnathan Karuppaiah · Date: 2024-09-10

![Biker Gopher](/i/blog/Social-Card_Dynamic_Image_Creation_banner.png)

Social-card: A dynamic image generator for business, profile, and social cards using Vercel Open Graph, Next.js, and TailwindCSS. Easily customize and create visually appealing cards for any purpose! 

## Features

::list{type="success"}
- **Business, Profile, and Social Cards:** Automatically generate profile cards for sharing across platforms.
- **QR Code Generation:** A built-in API to create QR codes that can be embedded in profile cards.
- **Image URL for Profile Cards:** Generate profile cards dynamically through URL parameters for easy sharing.
- **Edge Deployment:** Optimized for edge platforms like Vercel, ensuring low latency and high availability.
::

## Technology
- **Vercel Open Graph:** Enables dynamic card generation and sharing functionality.
- **Next.js:** Powers the serverless routes for the project, including the QR code generation API.

## Using Social Cards as Image URLs

You can dynamically generate and use social cards as image URLs by specifying the required parameters in the URL.

### URL Structure

```html 
http://localhost:3000/profile-card?name=<name>&email=<email>&mobile=<mobile>&title=<title>&profile_image_url=<profile_image_url>&website=<website>
```

### Parameters

- name: The full name of the person.
- email: The person's email address.
- mobile: The person's mobile number.
- title: The person's job title.
- profile_image_url: Optional. A publicly accessible URL to the profile image.
- website: A publicly accessible URL to the website or blog.
- bg_color: Optional. Tailwind css colors[indigo, orange, pink, yellow, teal, green], the default is indigo.
- bg_image_url: Optional. A publicly accessible URL to the background image

### Demo

```html 
https://social-card-five.vercel.app/profile-card?name=Biker%20Gopher&email=biker.gopher@email.com&mobile=%2B1%20222-222-2222&title=Solutions%20Architect&profile_image_url=https://github.com/ashleymcnamara/gophers/blob/master/Biker_Gopher.png?raw=true&website=www.senthilsweb.com&bg_color=pink
```

![img1](/i/blog/Social-Card_Dynamic_Image_Creation_1.png)

![img2](/i/blog/Social-Card_Dynamic_Image_Creation_2.png)

![img3](/i/blog/Social-Card_Dynamic_Image_Creation_3.png)

## Source Code

Check out the fully working examples with a detailed getting started readme guide on GitHub: https://github.com/senthilsweb/social-card