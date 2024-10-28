# Feature-3-Jade
import streamlit as st
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

# Function to simulate water consumption data
def generate_water_data(days):
    # Simulate water consumption for each day (liters)
    water_usage = np.random.normal(150, 30, days)  # Average 150 liters per day with some variation
    return water_usage

# Function to generate a text summary of the water consumption
def generate_text_summary(water_usage):
    total_consumption = np.sum(water_usage)
    average_consumption = np.mean(water_usage)
    max_consumption = np.max(water_usage)
    min_consumption = np.min(water_usage)
    
    summary = (
        f"Total Water Consumed: {total_consumption:.2f} liters\n"
        f"Average Daily Consumption: {average_consumption:.2f} liters\n"
        f"Maximum Daily Consumption: {max_consumption:.2f} liters\n"
        f"Minimum Daily Consumption: {min_consumption:.2f} liters"
    )
    return summary

# Streamlit App
st.title("Water Consumption Monitoring")
st.write("Track the amount of water consumed from the faucet over time.")

# User inputs for configuration
days = st.slider("Select the number of days to simulate:", min_value=7, max_value=30, value=14)

# Generate water consumption data
water_usage = generate_water_data(days)

# Display text summary
st.subheader("Water Consumption Summary")
summary = generate_text_summary(water_usage)
st.text(summary)

# Plot water consumption data
st.subheader("Water Consumption Over Time")
fig, ax = plt.subplots()
ax.plot(range(1, days + 1), water_usage, marker='o', linestyle='-', color='b')
ax.set_title('Daily Water Consumption')
ax.set_xlabel('Day')
ax.set_ylabel('Water Consumption (liters)')
st.pyplot(fig)

# Generate an image representation of water usage (optional)
st.subheader("Image Representation of Water Consumption")
water_level_image = np.zeros((100, days, 3), dtype=np.uint8)

# Create a bar-like visual representation
for i, usage in enumerate(water_usage):
    level = int(usage / max(water_usage) * 100)
    water_level_image[100 - level:, i, :] = [0, 0, 255]  # Blue color for water

# Display the generated image
st.image(water_level_image, caption="Water Consumption Bar Image", use_column_width=True)
