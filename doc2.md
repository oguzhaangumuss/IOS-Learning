# 🏛️ NFT Marketplace Smart Contract Documentation  

## 📁 Project Structure  

src/
├── lib.rs           // Program entry point
├── instructions.rs  // Instruction handlers and account validation
├── state.rs         // Program state and account structures
├── errors.rs        // Custom error definitions
├── events.rs        // Event definitions
└── utils/
├── mod.rs       // Utils module definition
├── constants.rs // Program constants
└── transfers.rs // Token transfer utilities

---

## 🔧 Core Components  

### 1️⃣ **State Management (`state.rs`)**  
```rust
pub struct Listing {
    pub seller: Pubkey,    // NFT seller's public key
    pub price: u64,        // Listing price in SOL
    pub mint: Pubkey,      // NFT mint address
    pub is_active: bool,   // Listing status
}

	•	Implements initialize method for safe state initialization
	•	Includes space calculation for account allocation

2️⃣ Instructions (instructions.rs)

📌 Account Validation Structs:
	•	ListNFT → NFT listing creation
	•	RemoveListedNFT → Listing removal
	•	BuyNFT → NFT purchase

🔍 Helper Modules:
	•	validation.rs → Price & NFT balance validation
	•	events.rs → Event emission helpers
	•	accounts.rs → Account validation structs

🛠 Instruction Handlers:

✅ list_nft
	•	Validates price and NFT balance
	•	Transfers NFT to vault
	•	Initializes listing state
	•	Emits ListingCreated event

✅ remove_listed_nft
	•	Returns NFT to seller
	•	Closes listing account
	•	Emits ListingCancelled event

✅ buy_nft
	•	Transfers SOL to seller
	•	Transfers NFT to buyer
	•	Updates listing status
	•	Emits NFTPurchased event

3️⃣ Events (events.rs)
	•	ListingCreated → When new NFT is listed
	•	ListingCancelled → When listing is removed
	•	NFTPurchased → When NFT is sold

4️⃣ Error Handling (errors.rs)
ErrorCode {
    InactiveListing,
    InvalidPrice,
    InsufficientBalance,
    InvalidTokenAccountOwner,
    Unauthorized,
}

5️⃣ Utils (utils/)
	•	constants.rs → Program-wide constants
	•	transfers.rs → Token transfer helper functions

🔐 Security Features

✔️ Account validation checks
✔️ Owner verification
✔️ Balance verification
✔️ Token program checks
✔️ PDA (Program Derived Address) for vault accounts

💡 Recent Optimizations
	•	✅ Modular code structure
	•	✅ Centralized state initialization
	•	✅ Helper functions for common operations
	•	✅ Event handling abstraction
	•	✅ Clear error definitions

🔄 Program Flow

🟢 Listing NFT: 
User -> ListNFT -> Validate -> Transfer to Vault -> Initialize State -> Emit Event

🔴 Removing Listing:
User -> RemoveListedNFT -> Transfer to Seller -> Close Account -> Emit Event

🔵 Buying NFT:
User -> BuyNFT -> Transfer SOL -> Transfer NFT -> Update State -> Emit Event

📝 Best Practices Implemented

✅ Clear separation of concerns
✅ Comprehensive error handling
✅ Event-driven architecture
✅ Secure token transfers
✅ Efficient state management
✅ Modular code organization
✅ Proper validation checks

🛠 Development Notes
	•	🔹 Built with Anchor framework
	•	🔹 Uses Token Program 2022
	•	🔹 Implements SPL Token interface
	•	🔹 Uses Program Derived Addresses (PDAs)
	•	🔹 Follows Solana program development best practices