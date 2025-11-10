from kivy.app import App
from kivy.uix.label import Label
from kivy.uix.boxlayout import BoxLayout
from kivy.uix.button import Button
from kivy.uix.textinput import TextInput


class Area(App):
    def build(self):
        
        main_layout = BoxLayout(orientation='vertical', padding=(50, 50, 50, 50), spacing=20)

        
        self.t_label = Label(text="Area Calculator", font_size=50)
        main_layout.add_widget(self.t_label)

        
        self.length = TextInput(hint_text="Enter the length", font_size="50dp", multiline=False, input_filter='float')
        self.width = TextInput(hint_text="Enter the width", font_size="50dp", multiline=False, input_filter='float')

        main_layout.add_widget(self.length)
        main_layout.add_widget(self.width)

        
        button_layout = BoxLayout(orientation='horizontal', spacing=20, size_hint=(1, 0.3))

        self.sbn_btn = Button(text="Calculate", font_size=40)
        self.clr_btn = Button(text="Clear", font_size=40)

        
        button_layout.add_widget(self.sbn_btn)
        button_layout.add_widget(self.clr_btn)

        
        main_layout.add_widget(button_layout)

        
        self.sbn_btn.bind(on_press=self.answer)
        self.clr_btn.bind(on_press=self.clear)

        return main_layout

    def answer(self, instance):
        try:
            length_val = float(self.length.text)
            width_val = float(self.width.text)
            result = length_val * width_val
            self.t_label.text = f"The area is {result:,}"
        except ValueError:
            self.t_label.text = "Please enter valid numbers!"

    def clear(self, instance):
        self.length.text = ""
        self.width.text = ""
        self.t_label.text = "Area Calculator"


if __name__ == '__main__':
    Area().run()