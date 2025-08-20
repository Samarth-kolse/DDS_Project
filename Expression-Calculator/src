#include <bits/stdc++.h>
using namespace std;

struct Token {
    enum Type { NUMBER, OP, LPAREN, RPAREN } type;
    string text;
    double value;
};

static bool isop(char c){ return c=='+'||c=='-'||c=='*'||c=='/'||c=='^'; }
static bool isdigitdot(char c){ return (c>='0'&&c<='9')||c=='.'; }

static vector<Token> tokenize(const string& s){
    vector<Token> out;
    for(size_t i=0;i<s.size();){
        if(isspace((unsigned char)s[i])){ i++; continue; }
        if(s[i]=='('){ out.push_back({Token::LPAREN,"(",0}); i++; continue; }
        if(s[i]==')'){ out.push_back({Token::RPAREN,")",0}); i++; continue; }
        if(isop(s[i])){
            string t(1,s[i]);
            out.push_back({Token::OP,t,0});
            i++; continue;
        }
        if(isdigitdot(s[i])){
            size_t j=i; bool dot=false;
            while(j<s.size() && isdigitdot(s[j])){
                if(s[j]=='.'){ if(dot) break; dot=true; }
                j++;
            }
            string num = s.substr(i,j-i);
            out.push_back({Token::NUMBER,num,stod(num)});
            i=j; continue;
        }
        if(isalpha((unsigned char)s[i])){
            size_t j=i;
            while(j<s.size() && (isalnum((unsigned char)s[j])||s[j]=='_')) j++;
            throw runtime_error("unexpected identifier: "+s.substr(i,j-i));
        }
        throw runtime_error(string("unexpected character: ")+s[i]);
    }
    return out;
}

struct OpInfo { int prec; bool right; int arity; };
static OpInfo opinfo(const string& op){
    if(op=="~") return {4,true,1};
    if(op=="^") return {3,true,2};
    if(op=="*"||op=="/") return {2,false,2};
    if(op=="+"||op=="-") return {1,false,2};
    throw runtime_error("unknown operator: "+op);
}

static vector<Token> to_postfix(const vector<Token>& in){
    vector<Token> out;
    vector<Token> st;
    Token prev{Token::LPAREN,"(",0};
    for(size_t i=0;i<in.size();++i){
        Token t = in[i];
        if(t.type==Token::NUMBER){ out.push_back(t); prev=t; continue; }
        if(t.type==Token::LPAREN){ st.push_back(t); prev=t; continue; }
        if(t.type==Token::RPAREN){
            bool ok=false;
            while(!st.empty()){
                Token u=st.back(); st.pop_back();
                if(u.type==Token::LPAREN){ ok=true; break; }
                out.push_back(u);
            }
            if(!ok) throw runtime_error("mismatched parentheses");
            prev=t; continue;
        }
        if(t.type==Token::OP){
            string op = t.text;
            if(op=="-" && (prev.type==Token::LPAREN || prev.type==Token::OP)) op="~";
            OpInfo oi = opinfo(op);
            Token asOp{Token::OP,op,0};
            while(!st.empty() && st.back().type==Token::OP){
                OpInfo topi = opinfo(st.back().text);
                if( (oi.right && oi.prec<topi.prec) || (!oi.right && oi.prec<=topi.prec) ){
                    out.push_back(st.back()); st.pop_back();
                } else break;
            }
            st.push_back(asOp);
            prev=asOp; continue;
        }
        throw runtime_error("invalid token stream");
    }
    while(!st.empty()){
        if(st.back().type==Token::LPAREN) throw runtime_error("mismatched parentheses");
        out.push_back(st.back()); st.pop_back();
    }
    return out;
}

static double eval_postfix(const vector<Token>& pf){
    vector<double> st;
    for(const auto& t: pf){
        if(t.type==Token::NUMBER){ st.push_back(t.value); continue; }
        if(t.type==Token::OP){
            OpInfo oi = opinfo(t.text);
            if((int)st.size()<oi.arity) throw runtime_error("insufficient operands");
            if(oi.arity==1){
                double a=st.back(); st.pop_back();
                if(t.text=="~") st.push_back(-a);
                else throw runtime_error("unknown unary op");
            }else{
                double b=st.back(); st.pop_back();
                double a=st.back(); st.pop_back();
                if(t.text=="+") st.push_back(a+b);
                else if(t.text=="-") st.push_back(a-b);
                else if(t.text=="*") st.push_back(a*b);
                else if(t.text=="/"){ if(b==0.0) throw runtime_error("division by zero"); st.push_back(a/b); }
                else if(t.text=="^") st.push_back(pow(a,b));
                else throw runtime_error("unknown binary op");
            }
            continue;
        }
        throw runtime_error("invalid postfix token");
    }
    if(st.size()!=1) throw runtime_error("malformed expression");
    return st.back();
}

static double evaluate_expression(const string& expr){
    auto toks = tokenize(expr);
    vector<Token> normalized;
    Token prev{Token::LPAREN,"(",0};
    for(size_t i=0;i<toks.size();++i){
        Token t=toks[i];
        if(t.type==Token::OP && t.text=="+" && (prev.type==Token::LPAREN||prev.type==Token::OP)){ prev=t; continue; }
        normalized.push_back(t);
        prev=t;
    }
    auto pf = to_postfix(normalized);
    return eval_postfix(pf);
}

int main(int argc, char** argv){
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    try{
        string expr;
        if(argc>1){
            vector<string> parts;
            for(int i=1;i<argc;i++) parts.push_back(string(argv[i]));
            for(size_t i=0;i<parts.size();++i){ expr+=parts[i]; if(i+1<parts.size()) expr+=' '; }
        }else{
            string line;
            if(!getline(cin,line)) return 0;
            expr=line;
        }
        double ans = evaluate_expression(expr);
        cout.setf(std::ios::fixed); cout<<setprecision(10)<<ans<<"\n";
        return 0;
    }catch(const exception& e){
        cerr<<"error: "<<e.what()<<"\n";
        return 1;
    }
}
