# InputField

1 import:

    import InputField from "@/components/InputField.vue";

2 declare:

    <InputField
        v-model="formData.name"
        className="form-control"
        :errors="v$.name.$errors"
        placeholder="Insert your name..."
    />

2.1 if you want to use mask, just insert the mask attribute:

    <InputField
        mask="(##) #####-####"
        v-model="formData.name"
        className="form-control"
        :errors="v$.name.$errors"
        placeholder="Insert your name..."
    />

3 you'll have something like this:

![Alt text](../images/input-field-1.png?raw=true "Input Field 1")

3.1 if you're using mask:

![Alt text](../images/input-field-2.png?raw=true "Input Field 2")
