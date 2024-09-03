import google.generativeai as genai
import streamlit as st
import os
GOOGLE_API_KEY = "AIzaSyAZJwz80npidKL-PT2oFRwQrEPFkCySVv0"

genai.configure(api_key=GOOGLE_API_KEY)
model = genai.GenerativeModel('gemini-1.5-flash')
def get_chatbot_response(user_input):
    response=model.generate_content(user_input)
    return response.text
st.title("🥰My Chatbot🥰")
st.write("Powered by Google Generative AI")
if "history" not in st.session_state:
        st.session_state["history"]=[]
# user_input= input("Enter your Prompt =")
# output=getResponseFromModel(user_input)
# print(output)
with st.form(key="chat_form",clear_on_submit=True):
    user_input =st.text_input("Your Prompt",max_chars=2500)
    submit_button = st.form_submit_button("GO")
    if submit_button:
        if user_input:
            response = get_chatbot_response(user_input)
            st.session_state.history.append((user_input,response))
        else:
            st.warning("Please Enter A Prompt")
       
