# Outreachplus
Application 

import streamlit as st
import pandas as pd
from datetime import datetime

# Set page config
st.set_page_config(page_title="NGO Connect", page_icon="🤝", layout="wide")

# Custom CSS for styling
st.markdown("""
    <style>
        .main {
            background-color: #f0f4f7;
        }
        .stButton button {
            background-color: #0a9396;
            color: white;
            font-weight: bold;
            border-radius: 8px;
            padding: 0.5em 1em;
        }
        .stTabs [data-baseweb="tab-list"] button {
            background-color: #e0fbfc;
            color: #005f73;
            font-weight: bold;
        }
    </style>
""", unsafe_allow_html=True)

st.title("🤝 NGO Donation & Volunteer Platform")
st.markdown("### Bridging donors, volunteers, and NGOs to create real impact 🌍")

# Sample NGO data
ngos = pd.DataFrame([
    {"NGO Name": "Helping Hands Trust", "Cause": "Education", "Location": "Mumbai"},
    {"NGO Name": "Jeevan Jyot Foundation", "Cause": "Health", "Location": "Ahmedabad"},
    {"NGO Name": "Annapurna Kitchen", "Cause": "Food Distribution", "Location": "Rajkot"},
    {"NGO Name": "Clean India Mission", "Cause": "Environment", "Location": "Delhi"},
])

# Store volunteers (for demo, not persistent)
volunteers = []

# Tabs
tab1, tab2, tab3 = st.tabs(["🏢 Browse NGOs", "🎁 Make a Donation", "🙋‍♂️ Join as Volunteer"])

# Tab 1: Browse NGOs
with tab1:
    st.subheader("Available NGOs")
    for _, row in ngos.iterrows():
        with st.container():
            st.markdown(f"""
                <div style="background-color:#ffffff;padding:15px;margin:10px 0;border-radius:10px;box-shadow:0 2px 5px rgba(0,0,0,0.1);">
                <h4 style="color:#0a9396;">{row['NGO Name']}</h4>
                <p><strong>Cause:</strong> {row['Cause']}<br>
                <strong>Location:</strong> {row['Location']}</p>
                </div>
            """, unsafe_allow_html=True)

# Tab 2: Donation Form
with tab2:
    st.subheader("Make a Donation")
    with st.form("donation_form"):
        col1, col2 = st.columns(2)
        with col1:
            name = st.text_input("Your Name")
            email = st.text_input("Email")
            donation_type = st.selectbox("Type of Donation", ["Money", "Food", "Clothes", "Books", "Others"])
        with col2:
            quantity = st.text_input("Amount / Quantity")
            ngo_selected = st.selectbox("Choose NGO", ngos["NGO Name"])
            date = st.date_input("Date of Donation", datetime.today())

        submitted = st.form_submit_button("Donate")

        if submitted:
            st.success(f"🎉 Thank you **{name}** for donating **{quantity} ({donation_type})** to **{ngo_selected}** on **{date}**!")

# Tab 3: Volunteer Form
with tab3:
    st.subheader("Join as a Volunteer")
    with st.form("volunteer_form"):
        col1, col2 = st.columns(2)
        with col1:
            name_v = st.text_input("Full Name")
            email_v = st.text_input("Email")
        with col2:
            skills = st.text_input("Your Skills or Interests")
            ngo_selected_v = st.selectbox("Which NGO would you like to volunteer for?", ngos["NGO Name"])

        submit_volunteer = st.form_submit_button("Submit Application")

        if submit_volunteer:
            volunteers.append({
                "name": name_v, "email": email_v, "skills": skills, "ngo": ngo_selected_v,
                "date": str(datetime.now().date())
            })
            st.success(f"✅ {name_v}, your volunteer application has been submitted to {ngo_selected_v}!")
