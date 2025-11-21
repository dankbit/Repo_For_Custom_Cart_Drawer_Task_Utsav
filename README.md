# Custom AJAX Cart Drawer for Shopify


This repository contains a custom-built, AJAX-powered cart drawer designed for the Shopify Dawn theme. It fulfills all assignment requirements, focusing on smooth user experience, real-time updates, and responsiveness.

### 🚀 How to Test This Code


Follow these simple steps to see the cart drawer in action on a Shopify store (Dawn Theme):


**1. Open Theme Code:** Go to your Shopify Admin > Online Store > Themes > Actions > Edit Code.

**2. Create Section:** In the Sections folder, create a new file named custom-cart-drawer.liquid.

**3. Paste Code:** Copy the code from this repository's custom-cart-drawer.liquid file and paste it there. Save the file.

**4. Add to Layout:** Open layout/theme.liquid and add the section with the name "Custom Cart Drawer" in the footer.
<img width="334" height="142" alt="image" src="https://github.com/user-attachments/assets/8766b103-2173-4521-b59a-9933a4f3f9ea" />


**5. Adjust Settings:**
	- Go to the Theme Editor (Customize).

	- Click on Theme Settings (Gear icon) > Cart.

	- Change "Cart type" to Page (this disables the default drawer so the custom one works).
<img width="334" height="142" alt="image" src="https://github.com/user-attachments/assets/198e73d0-94b5-441c-9c6f-7cac5aa2a549" />


**6. Save:** Click Save. The new drawer will now appear when you click the cart icon or add an item.


---

### ✅ Assignment Requirements Checklist


**Core Requirements:**


**- Slide-in Drawer:** Smooth open/close transition triggered by the cart icon. - COMPLETED

**- Cart Item Display:** Shows product image, title, and dynamic quantity controls. - COMPLETED

**- AJAX Actions:** Add, update, and remove items happen instantly without reloading the page. - COMPLETED

**- Responsive Design:** Fully functional on both desktop and mobile. - COMPLETED

**- Subtotal & Checkout:** Real-time subtotal calculation and integrated checkout button. - COMPLETED


**Bonus Requirements:**


**- Upsell Section:** "You may also like" section with instant "Add to Cart" functionality. - COMPLETED

**- Smart Recommendations:** Logic to switch between API recommendations and fallback products. - COMPLETED

**- Session Storage:** The drawer remembers if it was open after a page reload. - COMPLETED


---

### ✨ Extra Features Added


Beyond the assignment scope, I implemented several enhancements to improve conversion and user experience:


**1. Free Shipping Progress Bar:**

<img width="402" height="169" alt="image" src="https://github.com/user-attachments/assets/82edc399-21c2-44ec-bd06-c5dc3d2752a8" />


	- A visual bar at the top that fills up as users add items.

	- It gamifies the shopping experience and encourages users to spend more to reach the threshold.

	- Displays a celebration message ("🎉 You've unlocked Free Shipping!") when the goal is met.


**2. Utility Quick-Actions:**

<img width="414" height="246" alt="image" src="https://github.com/user-attachments/assets/05185ccf-c587-4f47-a33b-4780c5fb9040" />




	- Located at the bottom of the drawer, I added three toggleable icons:
		- 📝 Order Note: Lets customers leave special instructions.

		- 🏷️ Discount Code: A dedicated field to input promo codes before checkout.

		- 📅 Delivery Date: Allows users to select a preferred delivery date.



**3. Smart Fallback Logic:**

<img width="403" height="423" alt="image" src="https://github.com/user-attachments/assets/c03ddb16-ba25-4066-b042-a0df47cbd6e9" />


	- If the Shopify Recommendations API fails or returns no data, the system automatically loads a manual collection defined in the settings, ensuring the Upsell section is never empty.




### 🧠 How It Works (Logic Breakdown)


Here is the logic behind every requirement implemented in the code:


**Slide-in Mechanism (Requirement: Smooth Drawer):**


	- Logic: CSS Transitions & Class Toggling.

	- How: The drawer sits off-screen using CSS (translateX). When triggered, JavaScript adds an .is-open class which smoothly slides the drawer into view using hardware-accelerated CSS transitions, ensuring no lag.


**Real-Time Updates (Requirement: AJAX Actions):**


	- Logic: The Fetch API (/cart/change.js).

	- How: When a user changes quantity or removes an item, the code sends a silent background request to Shopify. It receives the updated data (new prices, totals) and updates the HTML text instantly, bypassing the need for a page reload.


**Upsell Logic (Requirement: Recommended Products):**


	- Logic: Conditional API Chaining (Smart Fallback).

	- How: The system is "smart"—it first tries to fetch dynamic recommendations from Shopify's Product Recommendations API based on the first item in the cart. If the API returns nothing (or the cart is empty), it automatically switches to a "Fallback Collection" defined in the theme settings, ensuring the area is never empty.

 
**Upsell "Add to Cart" (Requirement: Instant Add):**


	- Logic: AJAX Post Request (/cart/add.js).

	- How: Clicking "Add" on a suggestion sends a specific command to Shopify to add that product variant. The drawer immediately re-fetches the cart data to show the new item in the list without the user leaving the drawer.

 
**Persistent State (Requirement: Session Storage):**


	- Logic: Browser Session API.

	- How: Every time the drawer opens or closes, we save a tiny "flag" (true or false) in the user's browser memory. If the user refreshes the page, the code checks this flag immediately and re-opens the drawer if it was previously open.

 
**Responsive Layout (Requirement: Mobile & Desktop):**


	- Logic: CSS Flexbox.

	- How: Instead of fixed sizes, I used Flexbox for the layout. This allows buttons (like "Checkout" and "View Cart") and product rows to stretch or shrink to fit any screen size perfectly, keeping alignment consistent on mobile phones and desktops.

 
**Visual Feedback (Requirement: Animations):**


	- Logic: CSS Keyframes & DOM Manipulation.

	- How: When an item is removed, we don't just delete it; we collapse its height and fade it out first. This gives the user visual confirmation that their action succeeded before the data updates.
