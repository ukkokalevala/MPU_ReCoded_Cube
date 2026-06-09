Smoothing Factor: Introduced smoothFactor to apply smoothing to angle changes, reducing sudden movements and making the transitions smoother.
Reduced Delay: Lowered the delay to 50ms to check if this interval provides smoother updates without visible stuttering.
Angle Calculation: Instead of directly using new angles, the code blends old and new angle values for a smoother experience.
Final Tips:
Use a lower smoothFactor (e.g., 0.8 or 0.7) for more smoothing if you still see stuttering.
