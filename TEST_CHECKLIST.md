# Manual test checklist

Use this list after starting MySQL, the backend (`uvicorn`), and the frontend (`npm run dev`).

## Tourist flow

| Test Case ID | Description                      | Input                   | Expected Output              | Result |
|---------------|----------------------------------|-------------------------|------------------------------|--------|
| TC-01        | Login with correct credentials    | ADMIN_EMAIL account (Firebase) | Redirect to dashboard        |        |
| TC-02        | Add duplicate place to plan      | Same place twice        | Prevent duplicate            |        |
| TC-03        | Invalid login                     | wrong password          | Error message               |        |
| TC-04        | Get all categories                | N/A                     | List of categories          |        |
| TC-05        | Get all places                    | N/A                     | List of places              |        |
| TC-06        | Get place by ID                  | Valid place ID          | Place details               |        |
| TC-07        | Get non-existent place            | Invalid place ID        | 404 Not Found               |        |
| TC-08        | Filter places by category         | Valid category ID       | List of places in category  |        |
| TC-09        | Create place with missing name    | N/A                     | Validation error            |        |
| TC-11        | Admin login success                | testadmin/testpass123 | Access token and type       |        |
| TC-12        | Admin login wrong password         | testadmin/wrongpass   | Password Not Found          |        |
| TC-13        | Admin login non-existent user      | nonexistent/testpass   | Username Not Found          |        |
| TC-14        | Admin login missing username       | N/A                     | Validation error            |        |
| TC-15        | Admin login missing password       | N/A                     | Validation error            |        |
| TC-16        | Admin logout                       | Valid admin token       | Success message             |        |
| TC-17        | Get current admin info without token | N/A                   | 401 Unauthorized            |        |
| TC-18        | Expired token handling             | Expired token           | 401 Unauthorized            |        |
| TC-19        | Malformed token handling           | Malformed token         | 401 Unauthorized            |        |
| TC-20        | Token with wrong format            | Wrong format            | 401 Unauthorized            |        |
| TC-21        | Creating place without name        | N/A                     | Validation error            |        |
| TC-22        | Creating place with invalid coordinates | Invalid coordinates  | Validation error            |        |
| TC-23        | Get place by ID                  | Valid place ID          | Place details               |        |
| TC-24        | Get non-existent place            | Invalid place ID        | 404 Not Found               |        |
| TC-25        | Filter places by category         | Valid category ID       | List of places in category  |        |
| TC-26        | Create visit plan                 | Valid session ID        | Success message             |        |
| TC-27        | Get existing visit plan           | Valid session ID        | Visit plan details          |        |
| TC-28        | Add item to visit plan            | Valid place ID          | Success message             |        |
| TC-29        | Add duplicate item to visit plan   | Valid place ID          | Error message               |        |
| TC-30        | Get non-existent visit plan       | Invalid session ID      | 404 Not Found               |        |
| TC-31        | Add item to visit plan            | Valid place ID          | Success message             |        |
| TC-32        | Add item already in visit plan    | Valid place ID          | Error message               |        |
| TC-33        | Clear visit plan                  | Valid session ID        | Success message             |        |


- [ ] Home page loads in under 3 seconds
- [ ] All 10 places display on the home page
- [ ] Category filter shows only matching places
- [ ] "All" filter reset works correctly
- [ ] No-results message appears for an empty category
- [ ] Clicking a place card navigates to detail page
- [ ] Detail page shows name, category, description, opening hours, travel tips, distance
- [ ] Leaflet map renders with a marker at the place location
- [ ] Reference marker at Piliyandala is visible on the map
- [ ] Polyline connects the two markers
- [ ] Overview map on home page shows all place markers
- [ ] 25 km boundary circle visible on overview map
- [ ] "Add to Plan" button adds place to plan
- [ ] Plan count badge on NavBar increments
- [ ] Visit Plan page shows added places in order
- [ ] Duplicate place cannot be added (button shows "✓ Added")
- [ ] Remove from plan works
- [ ] Clear all plan with confirmation works
- [ ] Plan persists after page navigation (session_id in localStorage)

## Admin flow

- [ ] Navigate to /admin/login
- [ ] Empty form submission shows validation errors
- [ ] Wrong username returns "Username Not Found" message
- [ ] Wrong password returns "Password Not Found" message
- [ ] Correct credentials (the Firebase account matching `ADMIN_EMAIL`) redirect to dashboard
- [ ] Dashboard lists all 10 places
- [ ] "Add New Place" modal opens
- [ ] Place with coordinates outside 25 km is rejected with error message
- [ ] New place appears in list after successful creation
- [ ] Edit place pre-fills form with existing data
- [ ] Delete shows confirmation and removes from list
- [ ] Logout clears token and redirects to login
- [ ] Accessing /admin/dashboard without token redirects to /admin/login
