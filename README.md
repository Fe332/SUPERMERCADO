import customtkinter as ctk
from tkinter import ttk
from tkinter import messagebox
import json
from datetime import datetime, timedelta
 
# Arquivos JSON para armazenar dados
DATA_FILE = 'supermarket_data.json'
HISTORY_FILE = 'sale_history.json'
 
# Função para carregar dados do JSON
def load_json(filename):
    try:
        with open(filename, 'r') as file:
            return json.load(file)
    except FileNotFoundError:
        return {}
 
# Função para salvar dados no JSON
def save_json(filename, data):
    with open(filename, 'w') as file:
        json.dump(data, file, indent=4)
 
# Carregar dados existentes
data = load_json(DATA_FILE)
history = load_json(HISTORY_FILE)
 
class SupermarketManagementSystem(ctk.CTk):
    def __init__(self):
        super().__init__()
        self.title("SUPERMERCADO PAGUE MENO$")
        self.geometry("800x600")
        ctk.set_appearance_mode("System")  # Aplica tema do sistema
        ctk.set_default_color_theme("blue")  # Define o tema padrão
 
        # Frame para o menu lateral
        self.menu_frame = ctk.CTkFrame(self, width=200)
        self.menu_frame.pack(side="left", fill="y")
 
        # Frame para a área de conteúdo
        self.content_frame = ctk.CTkFrame(self)
        self.content_frame.pack(side="right", expand=True, fill="both", padx=10, pady=10)
 
        # Botões do menu lateral
        menu_buttons = [
            ("FUNCIONÁRIOS", self.show_employees_tab),
            ("FORNECEDORES", self.show_suppliers_tab),
            ("HISTÓRICO DE VENDAS", self.show_sales_history_tab),
            ("CADASTRO DE PRODUTOS/ENTRADA", self.show_product_categories_tab),
            ("CONTROLE DE ESTOQUE", self.show_controle_de_estoque_tab),
            ("GESTÃO DE PERDAS", self.show_product_losses_tab),
            ("PREFERÊNCIAS DE CLIENTES", self.show_customer_preferences_tab),
            ("VENDAS SAZONAIS", self.show_seasonal_sales_tab),
            ("CONTROLE DE COMPRAS", self.show_purchase_control_tab),
            ("FORMAS DE PAGAMENTO", self.show_payment_methods_tab),
            ("PROMOÇÕES DA SEMANA", self.show_weekly_promotions_tab),
        ]
 
        for text, command in menu_buttons:
            button = ctk.CTkButton(self.menu_frame, text=text, command=command)
            button.pack(fill="x", padx=10, pady=5)
 
        # Dicionário para armazenar frames de cada seção
        self.frames = {}
 
        # Criação de todas as seções
        self.create_employees_tab()
        self.create_suppliers_tab()
        self.create_sales_history_tab()
        self.create_product_categories_tab()
        self.create_controle_de_estoque_tab()
        self.create_product_losses_tab()
        self.create_customer_preferences_tab()
        self.create_seasonal_sales_tab()
        self.create_purchase_control_tab()
        self.create_payment_methods_tab()
        self.create_weekly_promotions_tab()
 
        # Exibe a seção inicial
        self.show_employees_tab()
 
    def add_buttons(self, parent_frame):
        add_button = ctk.CTkButton(parent_frame, text="Adicionar", fg_color="green", text_color="white", command=self.add_item)
        add_button.pack(side="left", padx=5, pady=5)
 
        delete_button = ctk.CTkButton(parent_frame, text="Excluir", fg_color="red", text_color="white", command=self.delete_item)
        delete_button.pack(side="left", padx=5, pady=5)
 
        save_button = ctk.CTkButton(parent_frame, text="Salvar", fg_color="blue", text_color="white", command=self.save_item)
        save_button.pack(side="left", padx=5, pady=5)
 
    def create_employees_tab(self):
        employees_frame = ctk.CTkFrame(self.content_frame)
       
        ctk.CTkLabel(employees_frame, text="Nome:").grid(row=0, column=0, padx=10, pady=10)
        self.employee_name = ctk.CTkEntry(employees_frame)
        self.employee_name.grid(row=0, column=1, padx=10, pady=10)
 
        ctk.CTkLabel(employees_frame, text="ID:").grid(row=1, column=0, padx=10, pady=10)
        self.employee_id = ctk.CTkEntry(employees_frame)
        self.employee_id.grid(row=1, column=1, padx=10, pady=10)
 
        ctk.CTkLabel(employees_frame, text="Setor Responsável:").grid(row=2, column=0, padx=10, pady=10)
        self.employee_sector = ctk.CTkEntry(employees_frame)
        self.employee_sector.grid(row=2, column=1, padx=10, pady=10)

        ctk.CTkLabel(employees_frame, text="Endereço:").grid(row=3, column=0, padx=10, pady=10)
        self.employee_sector = ctk.CTkEntry(employees_frame)
        self.employee_sector.grid(row=3, column=1, padx=10, pady=10)

        ctk.CTkLabel(employees_frame, text="Data de Admissão:").grid(row=4, column=0, padx=10, pady=10)
        self.employee_sector = ctk.CTkEntry(employees_frame)
        self.employee_sector.grid(row=4, column=1, padx=10, pady=10)

        ctk.CTkLabel(employees_frame, text="Data de Saída:").grid(row=5, column=0, padx=10, pady=10)
        self.employee_sector = ctk.CTkEntry(employees_frame)
        self.employee_sector.grid(row=5, column=1, padx=10, pady=10)

        ctk.CTkLabel(employees_frame, text="Contato:").grid(row=6, column=0, padx=10, pady=10)
        self.employee_sector = ctk.CTkEntry(employees_frame)
        self.employee_sector.grid(row=6, column=1, padx=10, pady=10)

        ctk.CTkLabel(employees_frame, text="E-Mail:").grid(row=7, column=0, padx=10, pady=10)
        self.employee_sector = ctk.CTkEntry(employees_frame)
        self.employee_sector.grid(row=7, column=1, padx=10, pady=10)

        ctk.CTkLabel(employees_frame, text="Buscar:").grid(row=8, column=0, padx=10, pady=10)
        self.employee_sector = ctk.CTkEntry(employees_frame)
        self.employee_sector.grid(row=8, column=1, padx=10, pady=10)
 
        button_frame = ctk.CTkFrame(employees_frame)
        button_frame.grid(row=9, column=0, columnspan=2, pady=10)
        self.add_buttons(button_frame)
 
        # Armazena o frame para esta seção
        self.frames["employees"] = employees_frame
 
    def create_suppliers_tab(self):
        suppliers_frame = ctk.CTkFrame(self.content_frame)
 
        ctk.CTkLabel(suppliers_frame, text="Nome:").grid(row=0, column=0, padx=10, pady=10)
        self.supplier_name = ctk.CTkEntry(suppliers_frame)
        self.supplier_name.grid(row=0, column=1, padx=10, pady=10)
 
        ctk.CTkLabel(suppliers_frame, text="Contato:").grid(row=1, column=0, padx=10, pady=10)
        self.supplier_contact = ctk.CTkEntry(suppliers_frame)
        self.supplier_contact.grid(row=1, column=1, padx=10, pady=10)
 
        ctk.CTkLabel(suppliers_frame, text="Empresa:").grid(row=2, column=0, padx=10, pady=10)
        self.supplier_company = ctk.CTkEntry(suppliers_frame)
        self.supplier_company.grid(row=2, column=1, padx=10, pady=10)
 
        ctk.CTkLabel(suppliers_frame, text="CNPJ:").grid(row=3, column=0, padx=10, pady=10)
        self.supplier_name = ctk.CTkEntry(suppliers_frame)
        self.supplier_name.grid(row=3, column=1, padx=10, pady=10)
 
        ctk.CTkLabel(suppliers_frame, text="Busca/Categoria:").grid(row=4, column=0, padx=10, pady=10)
        self.supplier_contact = ctk.CTkEntry(suppliers_frame)
        self.supplier_contact.grid(row=4, column=1, padx=10, pady=10)
 
        button_frame = ctk.CTkFrame(suppliers_frame)
        button_frame.grid(row=5, column=0, columnspan=2, pady=10)
        self.add_buttons(button_frame)
 
        # Armazena o frame para esta seção
        self.frames["suppliers"] = suppliers_frame
 
 
    def create_sales_history_tab(self):
        sales_history_frame = ctk.CTkFrame(self.content_frame)
 
        self.sales_history_text = ctk.CTkTextbox(sales_history_frame)
        self.sales_history_text.pack(expand=True, fill='both', padx=10, pady=10)
 
        # Armazena o frame para esta seção
        self.frames["sales_history"] = sales_history_frame
        
 
    def create_product_categories_tab(self):
        product_categories_frame = ctk.CTkFrame(self.content_frame)
 
        ctk.CTkLabel(product_categories_frame, text="Produto:").grid(row=0, column=0, padx=10, pady=10)
        self.product_categories_name = ctk.CTkEntry(product_categories_frame)
        self.product_categories_name.grid(row=0, column=1, padx=10, pady=10)
 
        ctk.CTkLabel(product_categories_frame, text="Código:").grid(row=1, column=0, padx=10, pady=10)
        self.product_categories_code = ctk.CTkEntry(product_categories_frame)
        self.product_categories_code.grid(row=1, column=1, padx=10, pady=10)

        ctk.CTkLabel(product_categories_frame, text="Categoria:").grid(row=2, column=0, padx=10, pady=10)
        self.loss_product_name = ctk.CTkEntry(product_categories_frame)
        self.loss_product_name.grid(row=2, column=1, padx=10, pady=10)

        ctk.CTkLabel(product_categories_frame, text="Quantidade:").grid(row=3, column=0, padx=10, pady=10)
        self.loss_product_name = ctk.CTkEntry(product_categories_frame)
        self.loss_product_name.grid(row=3, column=1, padx=10, pady=10)

        ctk.CTkLabel(product_categories_frame, text="Preço de Compra:").grid(row=4, column=0, padx=10, pady=10)
        self.loss_product_name = ctk.CTkEntry(product_categories_frame)
        self.loss_product_name.grid(row=4, column=1, padx=10, pady=10)

        ctk.CTkLabel(product_categories_frame, text="Preço de Venda:").grid(row=5, column=0, padx=10, pady=10)
        self.loss_product_name = ctk.CTkEntry(product_categories_frame)
        self.loss_product_name.grid(row=5, column=1, padx=10, pady=10)

        ctk.CTkLabel(product_categories_frame, text="Especificação/Embalagem:").grid(row=6, column=0, padx=10, pady=10)
        self.loss_product_name = ctk.CTkEntry(product_categories_frame)
        self.loss_product_name.grid(row=6, column=1, padx=10, pady=10)

        ctk.CTkLabel(product_categories_frame, text="Data da Entrada:").grid(row=7, column=0, padx=10, pady=10)
        self.loss_product_name = ctk.CTkEntry(product_categories_frame)
        self.loss_product_name.grid(row=7, column=1, padx=10, pady=10)

        ctk.CTkLabel(product_categories_frame, text="Validade:").grid(row=8, column=0, padx=10, pady=10)
        self.loss_product_name = ctk.CTkEntry(product_categories_frame)
        self.loss_product_name.grid(row=8, column=1, padx=10, pady=10)
 
        ctk.CTkLabel(product_categories_frame, text="Observação:").grid(row=9, column=0, padx=10, pady=10)
        self.loss_observation = ctk.CTkEntry(product_categories_frame)
        self.loss_observation.grid(row=9, column=1, padx=10, pady=10)

        ctk.CTkLabel(product_categories_frame, text="Buscar:").grid(row=10, column=0, padx=10, pady=10)
        self.loss_observation = ctk.CTkEntry(product_categories_frame)
        self.loss_observation.grid(row=10, column=1, padx=10, pady=10)
 
        button_frame = ctk.CTkFrame(product_categories_frame)
        button_frame.grid(row=11, column=0, columnspan=2, pady=10)
        self.add_buttons(button_frame)
 
        # Armazena o frame para esta seção
        self.frames["product_categories"] = product_categories_frame

    def create_controle_de_estoque_tab(self):
        controle_de_estoque_frame = ctk.CTkFrame(self.content_frame)
 
        ctk.CTkLabel(controle_de_estoque_frame, text="Produto:").grid(row=0, column=0, padx=10, pady=10)
        self.controle_de_estoque_tab_name = ctk.CTkEntry(controle_de_estoque_frame)
        self.controle_de_estoque_tab_name.grid(row=0, column=1, padx=10, pady=10)
 
        ctk.CTkLabel(controle_de_estoque_frame, text="Código:").grid(row=1, column=0, padx=10, pady=10)
        self.controle_de_estoque_tab_name_code = ctk.CTkEntry(controle_de_estoque_frame)
        self.controle_de_estoque_tab_name_code.grid(row=1, column=1, padx=10, pady=10)
 
        ctk.CTkLabel(controle_de_estoque_frame, text="Quantidade:").grid(row=2, column=0, padx=10, pady=10)
        self.controle_de_estoque_tab_quantidade = ctk.CTkEntry(controle_de_estoque_frame)
        self.controle_de_estoque_tab_quantidade.grid(row=2, column=1, padx=10, pady=10)
 
        ctk.CTkLabel(controle_de_estoque_frame, text="Validade:").grid(row=3, column=0, padx=10, pady=10)
        self.controle_de_estoque_tab_validade = ctk.CTkEntry(controle_de_estoque_frame)
        self.controle_de_estoque_tab_validade.grid(row=3, column=1, padx=10, pady=10)
 
        ctk.CTkLabel(controle_de_estoque_frame, text="Preço de Compra:").grid(row=4, column=0, padx=10, pady=10)
        self.controle_de_estoque_tab_preço_de_compra = ctk.CTkEntry(controle_de_estoque_frame)
        self.controle_de_estoque_tab_preço_de_compra.grid(row=4, column=1, padx=10, pady=10)
 
        ctk.CTkLabel(controle_de_estoque_frame, text="Observação:").grid(row=5, column=0, padx=10, pady=10)
        self.controle_de_estoque_tab_observação = ctk.CTkEntry(controle_de_estoque_frame)
        self.controle_de_estoque_tab_observação.grid(row=5, column=1, padx=10, pady=10)
 
        ctk.CTkLabel(controle_de_estoque_frame, text="Alerta de Reposição:").grid(row=6, column=0, padx=10, pady=10)
        self.controle_de_estoque_tab_alerta_de_reposição = ctk.CTkEntry(controle_de_estoque_frame)
        self.controle_de_estoque_tab_alerta_de_reposição.grid(row=6, column=1, padx=10, pady=10)
 
        button_frame = ctk.CTkFrame(controle_de_estoque_frame)
        button_frame.grid(row=11, column=0, columnspan=2, pady=10)
        self.add_buttons(button_frame)
 
        # Armazena o frame para esta seção
        self.frames["controle_de_estoque"] = controle_de_estoque_frame
   
    def create_product_losses_tab(self):
        losses_frame = ctk.CTkFrame(self.content_frame)
 
        ctk.CTkLabel(losses_frame, text="Produto:").grid(row=0, column=0, padx=10, pady=10)
        self.loss_product_name = ctk.CTkEntry(losses_frame)
        self.loss_product_name.grid(row=0, column=1, padx=10, pady=10)
 
        ctk.CTkLabel(losses_frame, text="Código:").grid(row=1, column=0, padx=10, pady=10)
        self.loss_observation = ctk.CTkEntry(losses_frame)
        self.loss_observation.grid(row=1, column=1, padx=10, pady=10)
 
        ctk.CTkLabel(losses_frame, text="Quantidade:").grid(row=2, column=0, padx=10, pady=10)
        self.loss_observation = ctk.CTkEntry(losses_frame)
        self.loss_observation.grid(row=2, column=1, padx=10, pady=10)
 
        ctk.CTkLabel(losses_frame, text="Observação:").grid(row=3, column=0, padx=10, pady=10)
        self.loss_observation = ctk.CTkEntry(losses_frame)
        self.loss_observation.grid(row=3, column=1, padx=10, pady=10)
 
        aaa= ctk.IntVar()
        chek1 = ttk.Checkbutton (losses_frame,text='Defeito', variable= aaa)
        chek1.place(x=170, y=200 )
        bbb = ctk.IntVar
        chek2 = ttk.Checkbutton(losses_frame, text='Quebrado', variable=bbb)
        chek2.place(x = 170, y= 220)
        ccc=ctk.IntVar
        chek3 = ttk.Checkbutton(losses_frame, text='Vencido', variable=ccc)
        chek3.place(x= 170, y= 240)
 
     
        add_loss_button = ttk.Button(losses_frame, text="Registrar Perda", command=self.register)
        add_loss_button.place(x= 230, y= 300)
 
        button_frame = ctk.CTkFrame(losses_frame)
        button_frame.place(x= 80, y= 350)
        self.add_buttons(button_frame)
 
        # Armazena o frame para esta seção
        self.frames["product_losses"] = losses_frame
 
 
    def create_customer_preferences_tab(self):
        preferences_frame = ctk.CTkFrame(self.content_frame)
 
        ctk.CTkLabel(preferences_frame, text="Produto em Falta:").grid(row=0, column=0, padx=10, pady=10)
        self.missing_product = ctk.CTkEntry(preferences_frame)
        self.missing_product.grid(row=0, column=1, padx=10, pady=10)

        ctk.CTkLabel(preferences_frame, text="Observação:").grid(row=1, column=0, padx=10, pady=10)
        self.missing_product = ctk.CTkEntry(preferences_frame)
        self.missing_product.grid(row=1, column=1, padx=10, pady=10)
 
        button_frame = ctk.CTkFrame(preferences_frame)
        button_frame.grid(row=2, column=0, columnspan=2, pady=10)
        self.add_buttons(button_frame)
 
        # Armazena o frame para esta seção
        self.frames["customer_preferences"] = preferences_frame
 
    def create_seasonal_sales_tab(self):
        seasonal_sales_frame = ctk.CTkFrame(self.content_frame)
 
        ctk.CTkLabel(seasonal_sales_frame, text="Produto:").grid(row=0, column=0, padx=10, pady=10)
        self.seasonal_product_name = ctk.CTkEntry(seasonal_sales_frame)
        self.seasonal_product_name.grid(row=0, column=1, padx=10, pady=10)
 
        ctk.CTkLabel(seasonal_sales_frame, text="Código:").grid(row=1, column=0, padx=10, pady=10)
        self.seasonal_product_code = ctk.CTkEntry(seasonal_sales_frame)
        self.seasonal_product_code.grid(row=1, column=1, padx=10, pady=10)

        ctk.CTkLabel(seasonal_sales_frame, text="Comemoração:").grid(row=2, column=0, padx=10, pady=10)
        self.seasonal_product_code = ctk.CTkEntry(seasonal_sales_frame)
        self.seasonal_product_code.grid(row=2, column=1, padx=10, pady=10)

        ctk.CTkLabel(seasonal_sales_frame, text="Total de Itens:").grid(row=3, column=0, padx=10, pady=10)
        self.seasonal_product_code = ctk.CTkEntry(seasonal_sales_frame)
        self.seasonal_product_code.grid(row=3, column=1, padx=10, pady=10)

        ctk.CTkLabel(seasonal_sales_frame, text="Data de Início:").grid(row=4, column=0, padx=10, pady=10)
        self.seasonal_product_code = ctk.CTkEntry(seasonal_sales_frame)
        self.seasonal_product_code.grid(row=4, column=1, padx=10, pady=10)

        ctk.CTkLabel(seasonal_sales_frame, text="Data de Término:").grid(row=5, column=0, padx=10, pady=10)
        self.seasonal_product_code = ctk.CTkEntry(seasonal_sales_frame)
        self.seasonal_product_code.grid(row=5, column=1, padx=10, pady=10)
 
        button_frame = ctk.CTkFrame(seasonal_sales_frame)
        button_frame.grid(row=6, column=0, columnspan=2, pady=10)
        self.add_buttons(button_frame)
 
        # Armazena o frame para esta seção
        self.frames["seasonal_sales"] = seasonal_sales_frame
 
    def create_purchase_control_tab(self):
        purchase_control_frame = ctk.CTkFrame(self.content_frame)
 
        ctk.CTkLabel(purchase_control_frame, text="Produto:").grid(row=0, column=0, padx=10, pady=10)
        self.purchase_product_name = ctk.CTkEntry(purchase_control_frame)
        self.purchase_product_name.grid(row=0, column=1, padx=10, pady=10)

        ctk.CTkLabel(purchase_control_frame, text="Código:").grid(row=1, column=0, padx=10, pady=10)
        self.purchase_product_name = ctk.CTkEntry(purchase_control_frame)
        self.purchase_product_name.grid(row=1, column=1, padx=10, pady=10)

        ctk.CTkLabel(purchase_control_frame, text="Quantidade:").grid(row=2, column=0, padx=10, pady=10)
        self.purchase_product_name = ctk.CTkEntry(purchase_control_frame)
        self.purchase_product_name.grid(row=2, column=1, padx=10, pady=10)

        ctk.CTkLabel(purchase_control_frame, text="Valor:").grid(row=3, column=0, padx=10, pady=10)
        self.purchase_product_name = ctk.CTkEntry(purchase_control_frame)
        self.purchase_product_name.grid(row=3, column=1, padx=10, pady=10)
 
        ctk.CTkLabel(purchase_control_frame, text="Status:").grid(row=4, column=0, padx=10, pady=10)
        self.purchase_status = ttk.Combobox(purchase_control_frame, values=["Pendente", "Em andamento", "Finalizada"])
        self.purchase_status.grid(row=4, column=1, padx=10, pady=10)
 
        button_frame = ctk.CTkFrame(purchase_control_frame)
        button_frame.grid(row=5, column=0, columnspan=2, pady=10)
        self.add_buttons(button_frame)
 
        # Armazena o frame para esta seção
        self.frames["purchase_control"] = purchase_control_frame
 
    def create_payment_methods_tab(self):
        payment_methods_frame = ctk.CTkFrame(self.content_frame)
 
        ctk.CTkLabel(payment_methods_frame, text="Forma de Pagamento:").grid(row=0, column=0, padx=10, pady=10)
        self.payment_method = ttk.Combobox(payment_methods_frame, values=["Cartão Débito", "Cartão Crédito", "Dinheiro", "PIX"])
        self.payment_method.grid(row=0, column=1, padx=10, pady=10)
 
        button_frame = ctk.CTkFrame(payment_methods_frame)
        button_frame.grid(row=1, column=0, columnspan=2, pady=10)
        self.add_buttons(button_frame)
 
        # Armazena o frame para esta seção
        self.frames["payment_methods"] = payment_methods_frame
 
    def create_weekly_promotions_tab(self):
        weekly_promotions_frame = ctk.CTkFrame(self.content_frame)
 
        ctk.CTkLabel(weekly_promotions_frame, text="Evento:").grid(row=0, column=0, padx=10, pady=10)
        self.promotion_product_name = ctk.CTkEntry(weekly_promotions_frame)
        self.promotion_product_name.grid(row=0, column=1, padx=10, pady=10)
 
        ctk.CTkLabel(weekly_promotions_frame, text="Produto:").grid(row=1, column=0, padx=10, pady=10)
        self.promotion_product_code = ctk.CTkEntry(weekly_promotions_frame)
        self.promotion_product_code.grid(row=1, column=1, padx=10, pady=10)
 
        ctk.CTkLabel(weekly_promotions_frame, text="Código:").grid(row=2, column=0, padx=10, pady=10)
        self.promotion_product_code = ctk.CTkEntry(weekly_promotions_frame)
        self.promotion_product_code.grid(row=2, column=1, padx=10, pady=10)
 
        ctk.CTkLabel(weekly_promotions_frame, text="Observação:").grid(row=3, column=0, padx=10, pady=10)
        self.promotion_product_code = ctk.CTkEntry(weekly_promotions_frame)
        self.promotion_product_code.grid(row=3, column=1, padx=10, pady=10)
 
        button_frame = ctk.CTkFrame(weekly_promotions_frame)
        button_frame.grid(row=5, column=0, columnspan=2, pady=10)
        self.add_buttons(button_frame)
 
        # Armazena o frame para esta seção
        self.frames["weekly_promotions"] = weekly_promotions_frame
 
    def show_frame(self, frame_name):
        # Oculta todos os frames e exibe o frame solicitado
        for frame in self.frames.values():
            frame.pack_forget()
        self.frames[frame_name].pack(expand=True, fill="both")
 
    def show_employees_tab(self):
        self.show_frame("employees")
 
    def show_suppliers_tab(self):
        self.show_frame("suppliers")
 
    def show_sales_history_tab(self):
        self.show_frame("sales_history")
 
    def show_product_categories_tab(self):
        self.show_frame("product_categories")

    def show_controle_de_estoque_tab(self):
        self.show_frame("controle_de_estoque")
 
    def show_product_losses_tab(self):
        self.show_frame("product_losses")
 
    def show_customer_preferences_tab(self):
        self.show_frame("customer_preferences")
 
    def show_seasonal_sales_tab(self):
        self.show_frame("seasonal_sales")
 
    def show_purchase_control_tab(self):
        self.show_frame("purchase_control")
 
    def show_payment_methods_tab(self):
        self.show_frame("payment_methods")
 
    def show_weekly_promotions_tab(self):
        self.show_frame("weekly_promotions")
 
    # Métodos para adicionar, excluir e salvar dados podem ser implementados aqui
    def add_item(self):
        messagebox.showinfo("Adicionar", "Função de adicionar item.")
 
    def delete_item(self):
        messagebox.showinfo("Excluir", "Função de excluir item.")
 
    def save_item(self):
        messagebox.showinfo("Salvar", "Função de salvar item.")
 
if __name__ == "__main__":
    app = SupermarketManagementSystem()
    app.mainloop()
