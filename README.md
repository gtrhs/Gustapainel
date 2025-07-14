# Gustapainel
Venda painel 
import React, { useState } from "react";

const produtos = [
  { id: 1, nome: "Painel Full Capa - Variação 1", preco: 10.99 },
  { id: 2, nome: "Painel Full Capa - Variação 2", preco: 17.99 },
  { id: 3, nome: "Painel Full Capa - Variação 3", preco: 30.99 },
  { id: 4, nome: "Sensibilidade", preco: 14.99 },
];

const pixData = {
  chave: "12345678900@pix.com.br",
  qrCodeUrl:
    "https://chart.googleapis.com/chart?chs=250x250&cht=qr&chl=00020126580014br.gov.bcb.pix0136123456789000@pix.com.br5204000053039865405100.005802BR5925DOUGLAS DA SILVA6009SAO PAULO62290525REC687461F054AC41253743546304C8D4",
};

export default function Loja() {
  const [carrinho, setCarrinho] = useState([]);
  const [mostrarPix, setMostrarPix] = useState(false);

  function adicionarProduto(produto) {
    setCarrinho([...carrinho, produto]);
  }

  function total() {
    return carrinho.reduce((acc, prod) => acc + prod.preco, 0).toFixed(2);
  }

  return (
    <div style={{ fontFamily: "Arial, sans-serif", padding: 20 }}>
      <header
        style={{
          display: "flex",
          justifyContent: "space-between",
          marginBottom: 20,
        }}
      >
        <div>
          <h2>Minha Loja</h2>
        </div>
        <div style={{ display: "flex", alignItems: "center", gap: 15 }}>
          <div style={{ position: "relative" }}>
            <button
              style={{
                fontSize: 24,
                cursor: "pointer",
                background: "none",
                border: "none",
                position: "relative",
              }}
              onClick={() => alert("Itens no carrinho")}
              aria-label="Carrinho"
            >
              🛒
              {carrinho.length > 0 && (
                <span
                  style={{
                    position: "absolute",
                    top: -5,
                    right: -10,
                    background: "red",
                    color: "white",
                    borderRadius: "50%",
                    padding: "2px 6px",
                    fontSize: 12,
                    fontWeight: "bold",
                  }}
                >
                  {carrinho.length}
                </span>
              )}
            </button>
          </div>
          <button
            onClick={() => setMostrarPix(true)}
            disabled={carrinho.length === 0}
            style={{
              padding: "10px 20px",
              backgroundColor: carrinho.length === 0 ? "#ccc" : "#28a745",
              color: "white",
              border: "none",
              borderRadius: 5,
              cursor: carrinho.length === 0 ? "not-allowed" : "pointer",
            }}
          >
            Finalizar Compra
          </button>
        </div>
      </header>

      <main style={{ display: "flex", gap: 20, flexWrap: "wrap" }}>
        {produtos.map((produto) => (
          <div
            key={produto.id}
            style={{
              border: "1px solid #ddd",
              borderRadius: 8,
              padding: 15,
              width: 220,
              boxShadow: "2px 2px 5px rgba(0,0,0,0.1)",
            }}
          >
            <h3>{produto.nome}</h3>
            <p>R$ {produto.preco.toFixed(2)}</p>
            <button
              onClick={() => adicionarProduto(produto)}
              style={{
                padding: "8px 15px",
                backgroundColor: "#007bff",
                color: "white",
                border: "none",
                borderRadius: 5,
                cursor: "pointer",
              }}
            >
              Adicionar
            </button>
          </div>
        ))}
      </main>

      {mostrarPix && (
        <div
          style={{
            position: "fixed",
            top: 0,
            left: 0,
            width: "100vw",
            height: "100vh",
            backgroundColor: "white",
            display: "flex",
            flexDirection: "column",
            justifyContent: "center",
            alignItems: "center",
            padding: 20,
            zIndex: 9999,
          }}
        >
          <h2>Pagamento PIX</h2>
          <p>
            Total: <strong>R$ {total()}</strong>
          </p>
          <img
            src={pixData.qrCodeUrl}
            alt="QR Code PIX"
            style={{ width: 250, height: 250, marginBottom: 20 }}
          />
          <p>
            Chave PIX:{" "}
            <strong
              style={{ userSelect: "all", cursor: "pointer" }}
              onClick={() => {
                navigator.clipboard.writeText(pixData.chave);
                alert("Chave PIX copiada!");
              }}
              title="Clique para copiar"
            >
              {pixData.chave}
            </strong>
          </p>
          <button
            onClick={() => setMostrarPix(false)}
            style={{
              marginTop: 20,
              padding: "10px 20px",
              backgroundColor: "#dc3545",
              color: "white",
              border: "none",
              borderRadius: 5,
              cursor: "pointer",
            }}
          >
            Fechar
          </button>
        </div>
      )}
    </div>
  );
}![Screenshot_2025-07-14-08-09-43-788_com android chrome](https://github.com/user-attachments/assets/f4d06027-edcd-4569-90cb-8388f83f9b45)
